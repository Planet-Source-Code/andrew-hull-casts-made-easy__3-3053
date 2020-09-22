<div align="center">

## Casts Made Easy\!


</div>

### Description

A tutorial that explains and gives examples for static_cast, reinterpret_cast, const_cast, and dynamic_cast.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Andrew Hull](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/andrew-hull.md)
**Level**          |Intermediate
**User Rating**    |4.9 (69 globes from 14 users)
**Compatibility**  |C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+, UNIX C\+\+
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/andrew-hull-casts-made-easy__3-3053/archive/master.zip)





### Source Code

<H2><CENTER>Casts Made Easy!</CENTER></H2>
<P><CENTER>&nbsp;</CENTER></P>
<P><FONT FACE="Times New Roman">In C, casting was easy. You could
cast like you called a function:</FONT></P>
<P><B>int i = int('A');</B></P>
<P><FONT FACE="Times New Roman">You can also do this in C++. But
the only reason it's there is for backwards compatibility with
C. Casting like this will eventually cause havoc in a large program,
and it also only provides support for primitive types. In C++,
there is a set of 4 ANSI C++ casts: static_cast, reinterpret_cast,
const_cast, and (the much feared) dynamic_cast. Here I will provide
an explanation and example for each cast, to make them easier
to understand and possibly save some programs using C casting
:)</FONT></P>
<P><FONT FACE="Times New Roman"><HR ALIGN=LEFT></FONT></P>
<P><FONT FACE="Times New Roman">First, the simplest and most common,
static_cast. This cast simply converts from one data type to another.
The syntax is:</FONT></P>
<P><B>static_cast&lt;<I>new_type</I>&gt;(<I>argument</I>);</B></P>
<P><FONT FACE="Times New Roman">where <I>new_type</I> is the type
to be converted to, and <I>argument </I>is the data you wish to
convert. Converting my earlier example from C to C++ yields:</FONT></P>
<P><B>int i = static_cast&lt;int&gt;('A');</B></P>
<P><FONT FACE="Times New Roman">Note that <I>new_type</I> can
be any data type, primitive or user-defined. <I>argument</I> can
also be a variable:</FONT></P>
<P><B>char letter = 'A';<BR>
int i = static_cast&lt;int&gt;(letter);</B></P>
<P><FONT FACE="Times New Roman">That's all there really is to
static_cast.</FONT></P>
<P><FONT FACE="Times New Roman"><HR ALIGN=LEFT></FONT></P>
<P><FONT FACE="Times New Roman">The next type of (and hardest
to spell) cast is reinterpret_cast. Unlike static_cast, reinterpret_cast
doesn't actually change any data, it causes the data to be reinterpreted,
or looked at differently, by the compiler. The most common use
of reinterpret_cast is casting a void* pointer, such as the one
returned from malloc():</FONT></P>
<P><B>int* num = reinterpret_cast&lt;int*&gt;(malloc(100));</B></P>
<P><FONT FACE="Times New Roman">But then again, who needs malloc()
when you've got new? reinterpret_cast can be dangerous, however,
like in this example:</FONT></P>
<P><B><FONT FACE="Times New Roman">i</FONT>nt num = 5;<BR>
int* pNum = &amp;num;<BR>
double* pDouble = reinterpret_cast&lt;double*&gt;(pNum);<BR>
<BR>
cout &lt;&lt; *pDouble &lt;&lt; endl;</B></P>
<P><FONT FACE="Times New Roman">This outputs integer data as if
it were double (or floating point) data. Nothing but bad things
can result from that! You'll probably get a lot of garbage printed
to the screen.</FONT></P>
<P><FONT FACE="Times New Roman">The moral here? Be careful with
reinterpret_cast!</FONT></P>
<P><FONT FACE="Times New Roman"><HR ALIGN=LEFT></FONT></P>
<P><FONT FACE="Times New Roman">Next we'll look at const_cast.
const_cast is for adding/removing const from a variable. There
usually isn't a reason to do this, and if there is, it's probably
bad programming. However, every so often there's a situation that
you just can't get around, and have to use const_cast. (sorta
like goto). Here's a simple example:</FONT></P>
<P><B>void Display(int* data)<BR>
{<BR>
cout &lt;&lt; *data &lt;&lt; endl;<BR>
}</B></P>
<P><B>int main()<BR>
{<BR>
const int num = 5;<BR>
Display(const_cast&lt;int*&gt;(&amp;num));<BR>
<BR>
return 0;<BR>
}</B></P>
<P><FONT FACE="Times New Roman">If you don't use const_cast here,
the compiler will give you an error along the lines of &quot;no
match for function...&quot; because const data can't be passed
into non-const function data. Redundant? Yes. Avoidable? Yes.
Occasionally necessary? Yes.</FONT></P>
<P><FONT FACE="Times New Roman"><HR ALIGN=LEFT></FONT></P>
<P><FONT FACE="Times New Roman">Finally, it's time to tackle the
one no one else wants to: dynamic_cast. There's a lot of confusion
over what it does, why to use it, when to use it, etc. The formal
(i.e. newbie-scaring) description says that it &quot;is a polymorphic
cast that verifies the runtime type of the object being cast&quot;.
Ouch. To make it clearer, consider this example:</FONT></P>
<P><B>class Base<BR>
{<BR>
public<BR>
virtual void DoSomething() {cout &lt;&lt; &quot;Base&quot; &lt;&lt;
endl;}<BR>
};</B></P>
<P><B>class Derived : public Base<BR>
{<BR>
public:<BR>
virtual void DoSomething() {cout &lt;&lt; &quot;Derived&quot;
&lt;&lt; endl;}<BR>
};</B></P>
<P><B>int main()<BR>
{<BR>
Derived derived;<BR>
Base* pBase = &amp;derived;<BR>
// the base pointer points to a derived object. Legal, but confusing.</B></P>
<P><B>Derived* pDerived = dynamic_cast&lt;Derived*&gt;(pBase);<BR>
// because pBase is actually a pointer to a Derived at runtime,
the<BR>
// cast succeeds and pDerived is assigned the value of pBase</B></P>
<P><B>if (pDerived)<BR>
pDerived-&gt;DoSomething();<BR>
<BR>
else<BR>
cout &lt;&lt; &quot;Bad cast&quot; &lt;&lt; endl;<BR>
<BR>
return 0;<BR>
}</B></P>
<P>&nbsp;</P>
<P><FONT FACE="Times New Roman">In this example, the pointer to
Base was assigned the address of a Derived object. That's legal.
Then, a pointer to a Derived is declared. A check is performed
with dynamic_cast: if, at runtime, the argument (pBase) is of
type new_type (Derived), then dynamic_cast returns a pointer to
Derived with the value pBase. So, pDerived is assigned the value
of a base pointer which without a cast would be impossible.</FONT></P>
<P><FONT FACE="Times New Roman">dynamic_cast returns NULL if the
cast fails, so to prevent a memory leak ALWAYS check if the cast
succeeded with an if...else. Classes used with dynamic_cast must
have at least one virtual function.</FONT></P>
<P><FONT FACE="Times New Roman"><HR ALIGN=LEFT></FONT></P>
<P><FONT FACE="Times New Roman">Well, that's it. I hope you've
learned something from all of this! Please leave any comments/feedback
that come to mind, everything is appreciated! If you need anything
cleared up, please feel free to email me at kavutitan26@yahoo.com.
Enjoy!</FONT></P>
<P><FONT FACE="Times New Roman">-&gt;Andrew-&lt;</FONT>

