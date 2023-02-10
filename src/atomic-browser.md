# Accessing the Atomic-Server by using the Atomic-Browser

After installing your server you can access it with your browser.
By default, that's [`http://localhost:9883`](http://localhost:9883).<br/>
Fun fact: `&#9883;` is HTML entity code for the Atom icon: ⚛.

Alternatively use the demo installation at <a href="https://atomicdata.dev" target="_blank">atomicdata.dev</a>.

## The Homepage, Your Drive

The first screen should show you your [_Drive_](https://atomicdata.dev/classes/Drive).
You can think of this as your root folder.
It is the resource hosted at the root URL, effectively being the home page of your server.

## Quick Setup - Creating a User/Agent
There's an instruction on the screen about the `/setup` page.
Click this, and you'll get a screen showing an [_Invite_](https://atomicdata.dev/classes/Invite).
Normally, you could `Accept as new user`, but since you're running on `localhost`, you won't be able to use the newly created Agent on non-local Atomic-Servers.
Therefore, it may be best to create an Agent on some _other_ running server, such as the [demo Invite on AtomicData.dev](https://atomicdata.dev/invites/1).
And after that, copy the Secret from the `User settings` panel from AtomicData.dev, go back to your `localhost` version, and press `sign in`.
Paste the Secret, and voila! You're signed in.

Now, again go to `/setup`. This time, you can `Accept as {user}`.
After clicking, your Agent has gotten `write` rights for the Drive!
You can verify this by hovering over the description field, clicking the edit icon, and making a few changes.
You can also press the menu button (three dots, top left) and press `Data view` to see your agent after the `write` field.
Note that you can now edit every field.
You can also fetch your data now as various formats.

Try checking out the other features in the menu bar, and check out the `collections`.

Again, check out the [README](https://github.com/atomicdata-dev/atomic-data-rust/blob/master/server/README.md) for more information and guides!

But first, understand the two Views of the Browser.

## Understanding the two Views of the Browser
The Atomic Browser has two views

* Edit View `(Ctrl+E)`
* Data View `(Ctrl+D)`

After installation your browser will be in `Edit View`, also known as 'Data Definitions' View. This means you will be viewing, browsing and editing the Data Definitions.
A simple `Ctrl+D` will switch you to `Data View` which will hide the data definitions but instead make all the data occurrences visible for viewing, browsing and editing. Just use `(Ctrl+E)` to switch back.

Now, we are ready to create some data.

## Creating your first Atomic Data

Now, in Edit View, let's create a [_Class_](https://atomicdata.dev/classes/Class).
A Class represents an abstract concept, such as a `BlogPost` (which we'll do here).
We can do this in a couple of ways:

- Press the `+ icon` button on the left menu (only visible when logged in), and selecting Class
- Opening [Class](https://atomicdata.dev/classes/Class) and pressing `new class`
- Going to the [Classes Collection](https://atomicdata.dev/classes/) and pressing the plus icon

The result is the same: we end up with a form in which we can fill in some details.

Let's add a shortname (singular, lower case), and then a description.

After that, we'll add the `required` properties.
This form you're looking at is constructed by using the `required` and `recommended` Properties defined in `Class`.
We can use these same fields to generate our BlogPost resource!
Which fields would be required in a `BlogPost`?
A `name`, and a `description`, probably.

So click on the `+ icon` under `requires` and search for these Properties to add them.

Now, we can skip the `recommended` properties, and get right to saving our newly created `BlogPost` class.
So, press save, and now look at what you created.

Notice a couple of things:

- Your Class has its own URL.
- It has a `parent`, shown in the top of the screen. This has impact on the visibility and rights of your Resource. We'll get to that [later in the documentation](./hierarchy.md).

Now, go to the navigation bar, which is by default at the bottom of the window. Use its context menu to open the `Data View`.
This view gives you some more insight into your newly created data, and various ways in which you can serialize it.

## How can I see the members of a collection?

The members of a <a href="https://docs.atomicdata.dev/schema/collections.html" target="_blank">collection</a> are the actual data of that collection, and thus you need to be in [the Data View](#understanding-the-two-views-of-the-browser) `(Ctrl+D)` to see them.

> While in [the Data View](#understanding-the-two-views-of-the-browser), clicking on `collections` in the left menu brings you to the list of members of the `collections` class. Clicking on one of its members, for example `classes` will show you the list of classes.

Now let us do that again but with some View switching to notice how that might confuse you in the beginning: 

> So again, while in [the Data View](#understanding-the-two-views-of-the-browser), click on `collections` in the left menu. You will see all the collections. Now press `Ctrl+E`. As expected that brings you to the Edit View of the `collections` class. <br/>
But now, press `Ctrl+D`... where are the collections? Yet another View? No, this indeed is data of the `collections` class, only the metadata. What you were expecting to see is the `subject` data, which is one click away, namely the subject link on top of this list of metadata.

## There's more!

This was just a very brief introduction to Atomic Server, and its features.
There's quite a bit that we didn't dive in to, such as versioning, file uploads, the collaborative document editor and more...
But by clicking around you're likely to discover these features for yourself.

In the next page, we'll dive into how you can create an publish JSON-AD files.
