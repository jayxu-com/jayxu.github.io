---
id: 16053
title: 在Struts中使用Validator实现可配置的信息校验（一）
date: '2006-03-07T17:53:17+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=16053'
permalink: /2006/03/07/16053
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '1630'
dsq_thread_id:
    - '5295466002'
---

在Struts中对用户输入信息的校验一般在FromBean中进行（除非需要访问数据库进行诸如登录信息的校验，因为这是Action的工作），本文将阐述如何在Struts中实现可配置的信息校验。
<h2>一、在FormBean中手工实现</h2>
最简单的方法是直接在FormBean中重写ActionForm类的validate方法，validate方法签名如下：
<pre lang="java">public ActionErrors validate(ActionMapping mapping, HttpServletRequest req)</pre>
比如需要校验age字段必须填写数字：
<pre lang="java" class="">public ActionErrors validate(ActionMapping mapping, HttpServletRequest req){
  ActionErrors errors = new ActionErrors();

  String age = this.getAge();
  if(!this.isNumber(age)){ // isNumber() is not implemented
    errors.add(... , ...);
  }

  return errors;
}</pre>
在form提交后，容器会调用validate方法对表单数据进行校验，如果返回的ActionErrors为空（即校验通过），则将FormBean提交Action，否则重定向到提交form的页面。

这种方法实现简单，直观，容易测试、调试，但不可避免地存在以下缺点：

<em>1、很难重用，导致重复开发
</em>有很多校验逻辑在整个网站中是相同的，比如上述的数字校验，还有email校验、长度校验等等，而通过覆盖validate方法很难对这些校验过程进行重用，除非定义一些helper类封装校验方法（比如上述的isNumber()）。而当需要为另一个FormBean加入相同的校验逻辑时必须重复地覆盖validate方法

<em>2、难于扩展
</em>当要对一个表单增、删、改校验逻辑时必须修改validate方法，重新打包、部署

<em>3、不可配置
</em>因为校验逻辑硬编码于class文件中，运行时不可能做到灵活地配置校验逻辑

因此，Struts中加入了另一种更灵活的校验机制：
<h2>二、使用Validator</h2>
Validator提供了一种基于xml配置文件的校验模型，要使用这一模型必须做如下实现：

1、FormBean继承org.apache.struts.validator.ValidatorForm而不是ActionForm

2、不覆盖validate方法

3、创建validator-rules.xml及validation.xml文件

validator-rules.xml定义了可用来配置的校验逻辑，如：
<pre lang="xml"> &lt;form-validation&gt;
   &lt;global&gt;
      &lt;validator name="required"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateRequired"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
                  msg="errors.required"/&gt;
      &lt;validator name="requiredif"
                 classname="org.apache.struts.validator.FieldChecks"
                 method="validateRequiredIf"
                 methodParams="java.lang.Object,
                               org.apache.commons.validator.ValidatorAction,
                               org.apache.commons.validator.Field,
                               org.apache.struts.action.ActionMessages,
                               org.apache.commons.validator.Validator,
                               javax.servlet.http.HttpServletRequest"
                 msg="errors.required"/&gt;
      &lt;validator name="validwhen"
          msg="errors.required"
                 classname="org.apache.struts.validator.validwhen.ValidWhen"
                 method="validateValidWhen"
                 methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"/&gt;
      &lt;validator name="minlength"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateMinLength"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.minlength"
           jsFunction="org.apache.commons.validator.javascript.validateMinLength"/&gt;
      &lt;validator name="maxlength"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateMaxLength"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.maxlength"
           jsFunction="org.apache.commons.validator.javascript.validateMaxLength"/&gt;
      &lt;validator name="mask"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateMask"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.invalid"/&gt;
      &lt;validator name="byte"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateByte"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.byte"
       jsFunctionName="ByteValidations"/&gt;
      &lt;validator name="short"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateShort"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.short"
       jsFunctionName="ShortValidations"/&gt;
      &lt;validator name="integer"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateInteger"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.integer"
       jsFunctionName="IntegerValidations"/&gt;
      &lt;validator name="long"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateLong"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.long"/&gt;
      &lt;validator name="float"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateFloat"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.float"
       jsFunctionName="FloatValidations"/&gt;
      &lt;validator name="double"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateDouble"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.double"/&gt;
      &lt;validator name="date"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateDate"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.date"
       jsFunctionName="DateValidations"/&gt;
      &lt;validator name="intRange"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateIntRange"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends="integer"
                  msg="errors.range"/&gt;
      &lt;validator name="floatRange"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateFloatRange"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends="float"
                  msg="errors.range"/&gt;
      &lt;validator name="doubleRange"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateDoubleRange"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends="double"
                  msg="errors.range"/&gt;
      &lt;validator name="creditCard"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateCreditCard"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.creditcard"/&gt;
      &lt;validator name="email"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateEmail"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.email"/&gt;
      &lt;validator name="url"
            classname="org.apache.struts.validator.FieldChecks"
               method="validateUrl"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       org.apache.commons.validator.Validator,
                       javax.servlet.http.HttpServletRequest"
              depends=""
                  msg="errors.url"/&gt;
     &lt;!--
       This simply allows struts to include the validateUtilities into a page, it should
       not be used as a validation rule.
     --&gt;
     &lt;validator name="includeJavaScriptUtilities"
            classname=""
               method=""
         methodParams=""
              depends=""
                  msg=""
           jsFunction="org.apache.commons.validator.javascript.validateUtilities"/&gt;
      &lt;validator name="codeinput"
            classname="consultII.web.utils.MyValidator"
               method="validateCodeInput"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       javax.servlet.http.HttpServletRequest"
                  msg="errors.code"/&gt;
      &lt;validator name="userinfo"
            classname="consultII.web.utils.MyValidator"
               method="validateUserInfo"
         methodParams="java.lang.Object,
                       org.apache.commons.validator.ValidatorAction,
                       org.apache.commons.validator.Field,
                       org.apache.struts.action.ActionMessages,
                       javax.servlet.http.HttpServletRequest"
                  msg="errors.info"/&gt;
   &lt;/global&gt;
&lt;/form-validation&gt;
</pre>
该配置文件的具体格式请查阅Struts的<a href="http://struts.apache.org/struts-taglib/dev_validator.html">官方文档</a>。可以看出其中对很多常用的校验逻辑进行了封装，比如数字校验（92行到103行），长度校验（33行到56行）等。

而validation.xml则是Validator的核心，其中可对各个FormBean中需要校验字段及校验逻辑进行灵活的配置：
<pre lang="xml"> &lt;form-validation&gt;
   &lt;formset&gt;
      &lt;form name="login"&gt;
         &lt;field property="username" depends="required"/&gt;
         &lt;field property="password" depends="required"/&gt;
         &lt;field property="input" depends="required,codeinput"/&gt;
      &lt;/form&gt;
      &lt;form name="search"&gt;
        &lt;field property="keyword" depends="required"/&gt;
      &lt;/form&gt;
      &lt;form name="signin"&gt;
         &lt;field property="username" depends="required"/&gt;
         &lt;field property="password" depends="required"/&gt;
         &lt;field property="passagain" depends="required"/&gt;
         &lt;field property="question" depends="required,userinfo"/&gt;
         &lt;field property="answer" depends="required,userinfo"/&gt;
         &lt;field property="age" depends="required,integer"/&gt;
         &lt;field property="input" depends="required,codeinput"/&gt;
         &lt;field property="email" depends="email"/&gt;
      &lt;/form&gt;
      &lt;form name="ask"&gt;
         &lt;field property="content" depends="required"/&gt;
      &lt;/form&gt;
   &lt;/formset&gt;
&lt;/form-validation&gt;</pre>
具体格式可查阅<a href="http://struts.apache.org/struts-taglib/dev_validator.html">官方文档</a>，如上例，3到5行定义了需要对名为“loging”的FormBean的“username”、“password”分别进行“required”校验（即必填字段）。校验逻辑之间可以组合，如第6行的“required,codeinput”，定义了先进行required校验，通过了再进行codeinput校验。

与在validate方法内进行校验相比，使用Validator的优势就很明显了，可重用（从上述xml文件可以看出对很多字段都进行了required校验）；可灵活配置、扩展，只需修改validation.xml文件就可以改变校验逻辑。