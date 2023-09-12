---
id: 13164
title: 'About save/persist, update/merge in JPA/Hibernate'
date: '2011-12-15T22:55:56+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13164'
permalink: /2011/12/15/13164
views:
    - '5728'
duoshuo_thread_id:
    - '6.3356049352871E+18'
dsq_thread_id:
    - '4271400850'
---

<h2>Save VS Persist</h2>
<address>from <a href="https://hibernate.onjira.com/browse/HHH-1273" target="_blank">https://hibernate.onjira.com/browse/HHH-1273</a></address>
<blockquote>The persist() operation on Session is not cascaded at flush time. This is somewhat unexpected from a users point of view and very difficult to explain and understand (you need excellent knowledge of flushing and cascading). Reason #1 for removal.

The persist() operation in general does not return a database identifier. This is surprising, as the JPA spec clearly requires a persistent instance to have a database identifier value. Since persist() makes instances persistent, it has to have the same semantics for assigning identifiers as save(). Hence, I expect that once this mismatch is resolved in the expert group, the persist() method will return a database identifier. Everything else doesn't make much sense, given the current specification and documentation. Conclusion is that persist() will have the same signature as save(). Reason #2 for removal.

To document persist() properly I need a reason for its existence. Right now I'm telling readers/users to ignore it on the Session API, because it only complicates the situation with no benefit.</blockquote>
<h2>Update VS Merge</h2>
<address>from <a href="http://docs.jboss.org/hibernate/core/3.3/reference/en/html/objectstate.html#objectstate-saveorupdate" target="_blank">http://docs.jboss.org/hibernate/core/3.3/reference/en/html/objectstate.html#objectstate-saveorupdate</a></address>
<blockquote>Usually update() or saveOrUpdate() are used in the following scenario:
<ul>
	<li>the application loads an object in the first session</li>
	<li>the object is passed up to the UI tier</li>
	<li>some modifications are made to the object</li>
	<li>the object is passed back down to the business logic tier</li>
	<li>the application persists these modifications by calling update() in a second session</li>
</ul>
saveOrUpdate() does the following:
<ul>
	<li>if the object is already persistent in this session, do nothing</li>
	<li>if another object associated with the session has the same identifier, throw an exception</li>
	<li> if the object has no identifier property, save() it</li>
	<li> if the object's identifier has the value assigned to a newly instantiated object, save() it</li>
	<li> if the object is versioned by a &lt;version&gt; or &lt;timestamp&gt;, and the version property value is the same value assigned to a newly instantiated object, save() it</li>
	<li> otherwise update() the object</li>
</ul>
and merge() is very different:
<ul>
	<li>if there is a persistent instance with the same identifier currently associated with the session, copy the state of the given object onto the persistent instance</li>
	<li> if there is no persistent instance currently associated with the session, try to load it from the database, or create a new persistent instance</li>
	<li> the persistent instance is returned</li>
	<li> the given instance does not become associated with the session, it remains detached</li>
</ul>
</blockquote>