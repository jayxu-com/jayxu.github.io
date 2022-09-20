---
id: 11701
title: 'Learn Vim Progressively'
date: '2011-09-08T12:53:38+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=11701'
permalink: /2011/09/08/11701
aktt_notify_twitter:
    - 'yes'
views:
    - '4327'
aktt_tweeted:
    - '1'
shorturl:
    - 'http://goo.gl/TS7zu'
duoshuo_thread_id:
    - '6.3356048555828E+18'
dsq_thread_id:
    - '4420074788'
posturl_add_url:
    - 'yes'
---

原文在<a href="http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/" target="_blank">这里</a>

&nbsp;

<img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/uber_leet_use_vim.jpg" alt="Über leet use vim!" />
<div>

<abbr title="Too long; didn't read">tl;dr</abbr>: Want to learn vim (the best text editor known to human kind) the fastest way possible. I suggest you a way. Start by learning the minimal to survive, then integrate slowly all tricks.

</div>
<a href="http://www.vim.org/">Vim</a> the Six Billion Dollar editor
<blockquote>Better, Stronger, Faster.</blockquote>
Learn <a href="http://www.vim.org/">vim</a> and it will be your last text editor. There isn’t any better text editor I know. Hard to learn, but incredible to use.

I suggest you to learn it in 4 steps:
<ol>
	<li>Survive</li>
	<li>Feel comfortable</li>
	<li>Feel Better, Stronger, Faster</li>
	<li>Use vim superpowers</li>
</ol>
By the end of this journey, you’ll become a vim superstar.

But before we start, just a warning. Learning vim will be painful at first. It will take time. It will be a lot like playing a music instrument. Don’t expect to be more efficient with vim than with another editor in less than 3 days. In fact it will certainly take 2 weeks instead of 3 days.
<h2 id="st-level----survive">1<sup>st</sup> Level – Survive</h2>
<ol>
	<li>Install <a href="http://www.vim.org/">vim</a></li>
	<li>Launch vim</li>
	<li>DO NOTHING! Read.</li>
</ol>
In a standard editor, typing on the keyboard is enough to write something and see it on the screen. Not this time. Vim is in <em>Normal</em> mode. Let’s get in <em>Insert</em> mode. Type on the letter <pre class="inline:true decode:1 " >i</pre>.

You should feel a bit better. You can type letters like in a standard notepad. To get back in <em>Normal</em> mode just tap the <pre class="inline:true decode:1 " >ESC</pre> key.

You know how to switch between <em>Insert</em> and <em>Normal</em> mode. And now, the list of command you can use in <em>Normal</em> mode to survive:
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >i</pre> → <em>Insert</em> mode. Type <pre class="inline:true decode:1 " >ESC</pre> to return to Normal mode.</li>
	<li><pre class="inline:true decode:1 " >x</pre> → Delete the char under the cursor</li>
	<li><pre class="inline:true decode:1 " >:wq</pre> → Save and Quit (<pre class="inline:true decode:1 " >:w</pre> save, <pre class="inline:true decode:1 " >:q</pre> quit)</li>
	<li><pre class="inline:true decode:1 " >dd</pre> → Delete (and copy) current line</li>
	<li><pre class="inline:true decode:1 " >p</pre> → Paste</li>
</ul>
Recommended:
<ul>
	<li><pre class="inline:true decode:1 " >hjkl</pre> (highly recommended but not mandatory) → basic cursor move (←↓↑→). Hint: <pre class="inline:true decode:1 " >j</pre> look like a down arrow.</li>
	<li><pre class="inline:true decode:1 " >:help &lt;command&gt;</pre> → Show help about <pre class="inline:true decode:1 " >&lt;command&gt;</pre>, you can start using <pre class="inline:true decode:1 " >:help</pre> without anything else.</li>
</ul>
</blockquote>
Only 5 commands. This is very few to start. Once these command start to become natural (may be after a complete day), you should go on level 2.

But before, just a little remark on <em>Normal mode</em>. In standard editors, to copy you have to use the <pre class="inline:true decode:1 " >Ctrl</pre> key (<pre class="inline:true decode:1 " >Ctrl-c</pre> generally). In fact, when you press <pre class="inline:true decode:1 " >Ctrl</pre>, it is a bit like if all your key change meaning. With vim in Normal mode, it is a bit like if your <pre class="inline:true decode:1 " >Ctrl</pre> key is always pushed down.

A last word about notations:
<ul>
	<li>instead of writing <pre class="inline:true decode:1 " >Ctrl-λ</pre>, I’ll write <pre class="inline:true decode:1 " >&lt;C-λ&gt;</pre>.</li>
	<li>command staring by <pre class="inline:true decode:1 " >:</pre> will must end by <pre class="inline:true decode:1 " >&lt;enter&gt;</pre>. For example, when I write <pre class="inline:true decode:1 " >:q</pre> it means <pre class="inline:true decode:1 " >:q&lt;enter&gt;</pre>.</li>
</ul>
<h2 id="nd-level----feel-comfortable">2<sup>nd</sup> Level – Feel comfortable</h2>
You know the commands required for survival. It’s time to learn a few more commands. I suggest:
<ol>
	<li>Insert mode variations:
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >a</pre> → insert after the cursor</li>
	<li><pre class="inline:true decode:1 " >o</pre> → insert a new line after the current one</li>
	<li><pre class="inline:true decode:1 " >O</pre> → insert a new line before the current one</li>
	<li><pre class="inline:true decode:1 " >cw</pre> → replace from the cursor to the end the word</li>
</ul>
</blockquote>
</li>
	<li>Basic moves
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >0</pre> → go to first column</li>
	<li><pre class="inline:true decode:1 " >^</pre> → go to first non-blank character of the line</li>
	<li><pre class="inline:true decode:1 " >$</pre> → go to the end of line</li>
	<li><pre class="inline:true decode:1 " >g_</pre> → go to the last non-blank character of line</li>
	<li><pre class="inline:true decode:1 " >/pattern</pre> → search for <pre class="inline:true decode:1 " >pattern</pre></li>
</ul>
</blockquote>
</li>
	<li>Copy/Paste
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >P</pre> → paste before, remember <pre class="inline:true decode:1 " >p</pre> is paste after current position.</li>
	<li><pre class="inline:true decode:1 " >yy</pre> → copy current line, easier but equivalent to <pre class="inline:true decode:1 " >ddP</pre></li>
</ul>
</blockquote>
</li>
	<li>Undo/Redo
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >u</pre> → undo</li>
	<li><pre class="inline:true decode:1 " >&lt;C-r&gt;</pre> → redo</li>
</ul>
</blockquote>
</li>
	<li>Load/Save/Quit/Change File (Buffer)
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >:e &lt;path/to/file&gt;</pre> → open</li>
	<li><pre class="inline:true decode:1 " >:w</pre> → save</li>
	<li><pre class="inline:true decode:1 " >:saveas &lt;path/to/file&gt;</pre> → save to <pre class="inline:true decode:1 " >&lt;path/to/file&gt;</pre></li>
	<li><pre class="inline:true decode:1 " >:x</pre>, <pre class="inline:true decode:1 " >ZZ</pre> or <pre class="inline:true decode:1 " >:wq</pre> → save and quit (<pre class="inline:true decode:1 " >:x</pre> only save if necessary)</li>
	<li><pre class="inline:true decode:1 " >:q!</pre> → quit without saving, also <pre class="inline:true decode:1 " >:qa!</pre> to even if there are some modified hidden buffers.</li>
	<li><pre class="inline:true decode:1 " >:bn</pre> (resp. <pre class="inline:true decode:1 " >:bp</pre>) → show next (resp. previous) file (buffer)</li>
</ul>
</blockquote>
</li>
</ol>
Take the time to integrate all of these command. Once done, you should be able to do every thing you are able to do on other editors. But until now, it is a bit awkward. But follow me to the next level and you’ll see why.
<h2 id="rd-level----better-stronger-faster">3<sup>rd</sup> Level – Better. Stronger. Faster.</h2>
Congratulation reaching this far! We can start the interesting stuff. At level 3, we’ll only talk about command which are compatible with the old vi.
<h3 id="better">Better</h3>
Let’s look at how vim could help you to repeat yourself:
<ol>
	<li><pre class="inline:true decode:1 " >.</pre> → (dot) will repeat the last command,</li>
	<li>N&lt;command&gt; → will do the command N times.</li>
</ol>
Some examples, open a file and type:
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >2dd</pre> → will delete 2 lines</li>
	<li><pre class="inline:true decode:1 " >3p</pre> → will paste the text 3 times</li>
	<li><pre class="inline:true decode:1 " >100idesu [ESC]</pre> → will write “desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu desu “</li>
	<li><pre class="inline:true decode:1 " >.</pre> → Just after the last command will write again the 100 “desu “.</li>
	<li><pre class="inline:true decode:1 " >3.</pre> → Will write 3 “desu” (and not 300, how clever).</li>
</ul>
</blockquote>
<h3 id="stronger">Stronger</h3>
Knowing how to move efficiently with vim is <em>very</em> important. Don’t skip this section.
<ol>
	<li>N<pre class="inline:true decode:1 " >G</pre> → Go to line N</li>
	<li><pre class="inline:true decode:1 " >gg</pre> → shortcut for <pre class="inline:true decode:1 " >1G</pre>, go to the start of the file</li>
	<li><pre class="inline:true decode:1 " >G</pre> → Go to last line</li>
	<li>Word moves:
<blockquote>
<ol>
	<li><pre class="inline:true decode:1 " >w</pre> → go to the start of the following word,</li>
	<li><pre class="inline:true decode:1 " >e</pre> → go to the end of this word.</li>
</ol>
By default, word are composed of letter and the underscore character. Let’s call a WORD a group of letter separated by blank characters. If you want to consider WORDS, then just use uppercases:
<ol>
	<li><pre class="inline:true decode:1 " >W</pre> → go to the start of the following WORD,</li>
	<li><pre class="inline:true decode:1 " >E</pre> → go to the end of this WORD.</li>
</ol>
<img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/word_moves.jpg" alt="Word moves example" /></blockquote>
</li>
</ol>
Now let’s talk about very efficient moves:
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >%</pre> : Go to corresponding <pre class="inline:true decode:1 " >(</pre>, <pre class="inline:true decode:1 " >{</pre>, <pre class="inline:true decode:1 " >[</pre>.</li>
	<li><pre class="inline:true decode:1 " >*</pre> (resp. <pre class="inline:true decode:1 " >#</pre>) : go to next (resp. previous) occurrence of the word under the cursor</li>
</ul>
</blockquote>
Believe me, the last three commands are gold.
<h3 id="faster">Faster</h3>
Remember about the importance of vi moves? Here is the reason. Most commands can be used using the following general format:

<pre class="inline:true decode:1 " >&lt;start position&gt;&lt;command&gt;&lt;end position&gt;</pre>

For example : <pre class="inline:true decode:1 " >0y$</pre> means
<ul>
	<li><pre class="inline:true decode:1 " >0</pre> → go to the beginning of this line</li>
	<li><pre class="inline:true decode:1 " >y</pre> → yank from here</li>
	<li><pre class="inline:true decode:1 " >$</pre> → up to the end of this line</li>
</ul>
We also can do things like <pre class="inline:true decode:1 " >ye</pre>, yank from here to the end of the word. But also <pre class="inline:true decode:1 " >y2/foo</pre> yank up to the second occurrence of “foo”.

But what was true for <pre class="inline:true decode:1 " >y</pre> (yank), is also true for <pre class="inline:true decode:1 " >d</pre> (delete), <pre class="inline:true decode:1 " >v</pre> (visual select), <pre class="inline:true decode:1 " >gU</pre> (uppercase), <pre class="inline:true decode:1 " >gu</pre> (lowercase), etc…
<h2 id="th-level----vim-superpowers">4th Level – Vim Superpowers</h2>
With all preceding commands you should be comfortable to use vim. But now, here are the killer features. Some of these features were the reason I started to use vim.
<h3 id="move-on-current-line-0---f-f-t-t--">Move on current line: <pre class="inline:true decode:1 " >0</pre> <pre class="inline:true decode:1 " >^</pre> <pre class="inline:true decode:1 " >$</pre> <pre class="inline:true decode:1 " >f</pre> <pre class="inline:true decode:1 " >F</pre> <pre class="inline:true decode:1 " >t</pre> <pre class="inline:true decode:1 " >T</pre> <pre class="inline:true decode:1 " >,</pre> <pre class="inline:true decode:1 " >;</pre></h3>
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >0</pre> → go to column 0</li>
	<li><pre class="inline:true decode:1 " >^</pre> → go to first character on the line</li>
	<li><pre class="inline:true decode:1 " >$</pre> → go to the last character on the line</li>
	<li><pre class="inline:true decode:1 " >fa</pre> → go to next occurrence of the letter <pre class="inline:true decode:1 " >a</pre> on the line. <pre class="inline:true decode:1 " >,</pre> (resp. <pre class="inline:true decode:1 " >;</pre>) will seek for the next (resp. previous) occurrence.</li>
	<li><pre class="inline:true decode:1 " >t,</pre> → go just before the character <pre class="inline:true decode:1 " >,</pre>.</li>
	<li><pre class="inline:true decode:1 " >3fa</pre> → search the 3<sup>rd</sup> occurrence of <pre class="inline:true decode:1 " >a</pre> on this line.</li>
	<li><pre class="inline:true decode:1 " >F</pre> and <pre class="inline:true decode:1 " >T</pre> → like <pre class="inline:true decode:1 " >f</pre> and <pre class="inline:true decode:1 " >t</pre> but backward. <img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/line_moves.jpg" alt="Line moves" /></li>
</ul>
</blockquote>
A useful tip is: <pre class="inline:true decode:1 " >dt"</pre> → remove everything until the <pre class="inline:true decode:1 " >"</pre>.
<h3 id="zone-selection-actionaobject-or-actioniobject">Zone selection <pre class="inline:true decode:1 " >&lt;action&gt;a&lt;object&gt;</pre> or <pre class="inline:true decode:1 " >&lt;action&gt;i&lt;object&gt;</pre></h3>
These command can only be used after an operator of in visual mode. But they are very powerful. Their main pattern is:

<pre class="inline:true decode:1 " >&lt;action&gt;a&lt;object&gt;</pre> and <pre class="inline:true decode:1 " >&lt;action&gt;i&lt;object&gt;</pre>

Where action can be any action, for example, <pre class="inline:true decode:1 " >d</pre> (delete), <pre class="inline:true decode:1 " >y</pre> (yank), <pre class="inline:true decode:1 " >v</pre> (select in visual mode). And object can be: <pre class="inline:true decode:1 " >w</pre> a word, <pre class="inline:true decode:1 " >W</pre> a WORD (extended word), <pre class="inline:true decode:1 " >s</pre> a sentence, <pre class="inline:true decode:1 " >p</pre> a paragraph. But also, natural character such as <pre class="inline:true decode:1 " >"</pre>, <pre class="inline:true decode:1 " >'</pre>, <pre class="inline:true decode:1 " >)</pre>, <pre class="inline:true decode:1 " >}</pre>, <pre class="inline:true decode:1 " >]</pre>.

Suppose the cursor is on the first <pre class="inline:true decode:1 " >o</pre> of <pre class="inline:true decode:1 " >(map (+) ("foo"))</pre>.
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >vi"</pre> → will select <pre class="inline:true decode:1 " >foo</pre>.</li>
	<li><pre class="inline:true decode:1 " >va"</pre> → will select <pre class="inline:true decode:1 " >"foo"</pre>.</li>
	<li><pre class="inline:true decode:1 " >vi)</pre> → will select <pre class="inline:true decode:1 " >"foo"</pre>.</li>
	<li><pre class="inline:true decode:1 " >va)</pre> → will select <pre class="inline:true decode:1 " >("foo")</pre>.</li>
	<li><pre class="inline:true decode:1 " >v2i)</pre> → will select <pre class="inline:true decode:1 " >map (+) ("foo")</pre></li>
	<li><pre class="inline:true decode:1 " >v2a)</pre> → will select <pre class="inline:true decode:1 " >(map (+) ("foo"))</pre></li>
</ul>
</blockquote>
<img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/textobjects.png" alt="Text objects selection" />
<h3 id="select-rectangular-blocks-c-v">Select rectangular blocks: <pre class="inline:true decode:1 " >&lt;C-v&gt;</pre>.</h3>
Rectangular blocks are very useful to comment many lines of code. Typically: <pre class="inline:true decode:1 " >0&lt;C-v&gt;&lt;C-d&gt;I-- [ESC]</pre>
<ul>
	<li><pre class="inline:true decode:1 " >^</pre> → go to start of the line</li>
	<li><pre class="inline:true decode:1 " >&lt;C-v&gt;</pre> → Start block selection</li>
	<li><pre class="inline:true decode:1 " >&lt;C-d&gt;</pre> → move down (could also be <pre class="inline:true decode:1 " >jjj</pre> or <pre class="inline:true decode:1 " >%</pre>, etc…)</li>
	<li><pre class="inline:true decode:1 " >I-- [ESC]</pre> → write <pre class="inline:true decode:1 " >-- </pre> to comment each line</li>
</ul>
<img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/rectangular-blocks.gif" alt="Rectangular blocks" />

Not on windows you might have to use <pre class="inline:true decode:1 " >&lt;C-q&gt;</pre> instead of <pre class="inline:true decode:1 " >&lt;C-v&gt;</pre> if your clipboard is not empty.
<h3 id="completion-c-n-and-c-p">Completion: <pre class="inline:true decode:1 " >&lt;C-n&gt;</pre> and <pre class="inline:true decode:1 " >&lt;C-p&gt;</pre>.</h3>
In Insert mode, just type the start of a word, then type <pre class="inline:true decode:1 " >&lt;C-p&gt;</pre>, magic… <img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/completion.gif" alt="Completion" />
<h3 id="macros--qa-do-something-q-a-">Macros : <pre class="inline:true decode:1 " >qa</pre> do something <pre class="inline:true decode:1 " >q</pre>, <pre class="inline:true decode:1 " >@a</pre>, <pre class="inline:true decode:1 " >@@</pre></h3>
<pre class="inline:true decode:1 " >qa</pre> record your actions in the <em>register</em> <pre class="inline:true decode:1 " >a</pre>. Then <pre class="inline:true decode:1 " >@a</pre> will replay the macro saved into the register <pre class="inline:true decode:1 " >a</pre> as if you typed it. <pre class="inline:true decode:1 " >@@</pre> is a shortcut to replay the last executed macro.
<blockquote><em>Example</em>

On a line containing only the number 1, type this:
<ul>
	<li><pre class="inline:true decode:1 " >qaYp&lt;C-a&gt;q</pre>→
<ul>
	<li><pre class="inline:true decode:1 " >qa</pre> start recording.</li>
	<li><pre class="inline:true decode:1 " >Yp</pre> duplicate this line.</li>
	<li><pre class="inline:true decode:1 " >&lt;C-a&gt;</pre> increment the number.</li>
	<li><pre class="inline:true decode:1 " >q</pre> stop recording.</li>
</ul>
</li>
	<li><pre class="inline:true decode:1 " >@a</pre> → write 2 under the 1</li>
	<li><pre class="inline:true decode:1 " >@@</pre> → write 3 under the 2</li>
	<li>Now do <pre class="inline:true decode:1 " >100@@</pre> will create a list of increasing numbers until 103.</li>
</ul>
</blockquote>
<img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/macros.gif" alt="Macros" />
<h3 id="visual-selection-vvc-v">Visual selection: <pre class="inline:true decode:1 " >v</pre>,<pre class="inline:true decode:1 " >V</pre>,<pre class="inline:true decode:1 " >&lt;C-v&gt;</pre></h3>
We saw an example with <pre class="inline:true decode:1 " >&lt;C-v&gt;</pre>. There is also <pre class="inline:true decode:1 " >v</pre> and <pre class="inline:true decode:1 " >V</pre>. Once the selection made, you can:
<ul>
	<li><pre class="inline:true decode:1 " >J</pre> → join all lines together.</li>
	<li><pre class="inline:true decode:1 " >&lt;</pre> (resp. <pre class="inline:true decode:1 " >&gt;</pre>) → indent to the left (resp. to the right).</li>
	<li><pre class="inline:true decode:1 " >=</pre> → auto indent</li>
</ul>
<img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/autoindent.gif" alt="Autoindent" />

Add something at the end of all visually selected lines:
<ul>
	<li><pre class="inline:true decode:1 " >&lt;C-v&gt;</pre></li>
	<li>go to desired line (<pre class="inline:true decode:1 " >jjj</pre> or <pre class="inline:true decode:1 " >&lt;C-d&gt;</pre> or <pre class="inline:true decode:1 " >/pattern</pre> or <pre class="inline:true decode:1 " >%</pre> etc…)</li>
	<li><pre class="inline:true decode:1 " >$</pre> go to the end of line</li>
	<li><pre class="inline:true decode:1 " >A</pre>, write text, <pre class="inline:true decode:1 " >ESC</pre>.</li>
</ul>
<img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/append-to-many-lines.gif" alt="Append to many lines" />
<h3 id="splits-split-and-vsplit">Splits: <pre class="inline:true decode:1 " >:split</pre> and <pre class="inline:true decode:1 " >vsplit</pre>.</h3>
Here are the main commands, but you should look at <pre class="inline:true decode:1 " >:help split</pre>.
<blockquote>
<ul>
	<li><pre class="inline:true decode:1 " >:split</pre> → create a split (<pre class="inline:true decode:1 " >:vsplit</pre> create a vertical split)</li>
	<li><pre class="inline:true decode:1 " >&lt;C-w&gt;&lt;dir&gt;</pre> : where dir is any of <pre class="inline:true decode:1 " >hjkl</pre> or ←↓↑→ to change split.</li>
	<li><pre class="inline:true decode:1 " >&lt;C-w&gt;_</pre> (resp. <pre class="inline:true decode:1 " >&lt;C-w&gt;|</pre>) : maximise size of split (resp. vertical split)</li>
	<li><pre class="inline:true decode:1 " >&lt;C-w&gt;+</pre> (resp. <pre class="inline:true decode:1 " >&lt;C-w&gt;-</pre>) : Grow (resp. shrink) split</li>
</ul>
</blockquote>
<img src="http://yannesposito.com/Scratch/img/blog/Learn-Vim-Progressively/split.gif" alt="Split" />
<h2 id="conclusion">Conclusion</h2>
That was 90% of commands I use every day. I suggest you to learn no more than one or two new command per day. After two to three weeks you’ll start to feel the power of vim in your hands.

Learning Vim is more a matter of training than plain memorization. Fortunately vim comes with some very good tools and an excellent documentation. Run vimtutor until you are familiar with most basic commands. Also, you should read carefully this page: <pre class="inline:true decode:1 " >:help usr_02.txt</pre>.

Then, you will learn about <pre class="inline:true decode:1 " >!</pre>, folds, registers, the plugins and many other features. Learn vim like you’d learn piano and all should be fine.