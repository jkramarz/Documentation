# Personalizing with the Publisher

The Publisher is meant to make advanced newsletters. 
On top of that the Publisher makes personalization 
of your created e-mails very simple. Below, you'll
find a few personalization examples. 

## Use of variables

With Smarty it is easy to store and use variables. Remember though, that 
there are important rules to keep in mind while working with Smarty:

* Escape variables your users entered by adding |escape after the variable name, not everyone has good intentions!
* Smarty is capital sensitive. `{$profile.name}` is different than `{$profile.NAME}`;
* Curcly braces can be used as symbol with [literal](./personalization-functions-literal).

### Database variables

A personalization variable consists of a dollar sign `$`, profile or subprofile
and the name of the variable placed between curly braces.
The following variables can for example be used in a template
or document:

* `{$profile.name}`
* `{$profile.email}`
* `{$profile.aanhef}`

These personalization variables only work when you have
the exact same fields in your database. Of course, the 
receivers information must be stored in the database as 
well. If that's all set, you can use the variables like 
this:

```text
Dear {$profile.salutation} {$profile.name},

You receive this email, because you subscribed 
with the following email address: {$profile.email}.
```

### Template variables

You can also use extra personalization variables by adding them in the 
Template menu. Here you define the name, the value should be specified 
when creating the document. You can use the value with **{$property.name}**, 
where name is replaced with the name of the property.

Let's say you want to give users a score based on their purchases and 
put it in your email. You don't need the score later (if you do, save it 
to your database!). You can then set a template variable **score**, calculate 
and assign the score and use it with **{$property.score}**.

### Custom content

You can also send separate content to different
[selections](selections-introduction) in your database
with the handy [in_selection](./personalization-functions-in_selection)
and [in_miniselection](./personalization-functions-in_miniselection)
functions. 

## Escape

It's a difficult subject, but very important for you to grasp.
When you present the opportunity for customers to fill in their
details, such as name, city and email address, the majority of 
them will of course always fill in their correct data. However,
as with everything online, people will always try to do harm
by hacking or other forms of digital abuse. This means that 
you can in no way be sure that the information people fill in,
actually is safe data. When this scenario occurs, there is a 
possibility of very nasty things happening to you or your 
customers when sending out your mailing. 

Luckily, Smarty has this covered with the *|escape* modifier. 
With this modifier you can make sure that input is being 
converted to a neutral format that is safe to store in your 
database. It goes like this:

```text
Dear {$profile.salutation|escape} {$profile.name|escape},
    

You receive this email, because you subscribed 
with the following email address: {$profile.email|escape}.
```

Again, always take in consideration to use |escape when
using Smarty code in HTML code. Don't worry about Smarty
code (personalization) in text versions or subject lines:
the |escape modifier isn't needed here as it only applies
to html code.

## Curly braces

Our software automatically tracks curly braces as it 
indicates that Smarty code is being stated. However, 
sometimes you want to use curly braces just as symbols.
You have to write some code in order to make sure that
the software does not make a mistake by interpreting 
the curly braces as Smarty. You can do it in two ways:
you can use {ldelim} and {rdelim} or {literal} en 
{/literal}. The difference is that with literal you 
can turn of the Smarty engine for a whole set of text  
that goes in between these tags.

```text
{literal}
    I love {curly braces}!
{/literal}
```

## Where can you use personalization?

Almost everywhere. Check the list below
to get some inspiration:

* Subject line from email;
* In email and webdocuments
* Various email headers (from, CC, BCC, X-Mailer, etc.);
* Personalized website content;
* Webforms;
* Hyperlinks and mailto: linksl
* Follow-up actions;
* Etc.

## More information

* [Personalization variables overview](./personalization-variables.md)
* [Personalization modifiers overview](./personalization-modifiers.md)
* [Personalization functions overview](./personalization-functions.md)
