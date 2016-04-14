# Authentication/Authorization with Gems

## Learning Objectives

  1. Understand the landscape of gems that can be used to do authorization and authentication in Rails.

## Authentication vs Authorization

Two concepts that are related, often confused, but important to distinguish are authentication and authorization.

*Authentication* is determining who someone is. When I take money out of an ATM, the bank authenticates me with using two authentication factors: my PIN, and the secret key stored on the chip in my ATM card. Before I get on a plane, the TSA (the airline security organization in the U.S.) authenticates me by asking for my ID and using the extremely advanced facial recognition hardware embedded in human brains to verify that the ID matches my face. Usernames and passwords and credentials are all authentication things.

*Authorization* is determining if someone can do a particular thing. The bouncer at the club authenticates me by looking at my ID, and then authorizes me to enter by looking at the list (though I am more typically asked to leave the premises).

## Authentication

In the first half of this unit we learned how to roll our own authentication scheme.

Most security professionals will tell you NEVER to roll your own authentication logic as we did in the first half of the unit.  This is because as a young (or even experienced programmer) it's unlikely you are a match for the myriad of tricks hackers are going to use to try and hack into your site.  Forget to salt your passwords?  You're open to rainbow table attacks.  Use the wrong hashing algorithm?  You're open to brute force attacks.  Leave security to those who are experts at it!

There are two solutions to this problem.  One, which we've already learned is letting someone else take care of logging users in!  Rather than devoting your scare resources to solving a solved problem, user the omniauth gem and let one of the internet giants like Facebook deal with authentication by leveraging the oauth protocol.  If Facebook gets hacked, you probably wouldn't have been safer implementing your own authentication scheme...

Along the same lines as this solution, is leveraging the Rails communities open source nature and using a battle tested gem to implement authentication.  In the same way using the omniauth gem can help you avoid implementing the oauth specification correctly yourself, there are a host of gems the Rails community has built over the years to help you avoid implementing authentication and authorization yourself.

One of the gems everybody loves almost as much as they hate it is Devise.  It's without a doubt the leader in the authentication space, and has over 3,000 commits in it's 7 year history.  It's heavily metaprogrammed, modularized and has a solution to just about any need your authentication scheme might require.  Our biggest complaint with devise is that it often obscures what's going on due to its metaprogramming, which makes it hard to change if it's configuration options don't account for EXACTLY your use case.  The great thing about Devise is it also offers some authorization options as well.

Other gems worth looking at in this space are [Warden](https://github.com/hassox/warden) (which devise is based around) and [Authlogic](https://github.com/binarylogic/authlogic)

## Authorization

Hey, can I delete this file?

It's a surprisingly loaded question. Did I create the file? Do I own it? What does it mean to own a file? Can I write to the file? If I can write to a thing, can I delete it?

These are questions of authorization.

Authorization deals with WHAT a user is allowed to do, once we know WHO that user is.  Can this particular user delete a post?  Can they view posts written by other users?  Authorization helps you answer these questions.

Although Devise doesn't have out of the box support for authorization, it's common to implement "roles" using Devise.  Roles allow us to segment our users into types or kinds of users.  For example, admins, teachers, and students.  By leveraging ActiveRecord's enum feature, you can define a user as having a specific role.  If you have simple enough authorization requirements this might be enough.  However, if your roles get more complicated you might want to bring in another gem to do the heavy lifting [Rolify](https://github.com/RolifyCommunity/rolify).

You can pair the concept of roles with other gems that allow you to specify what "abilities" or "policies" users or types of users.  For example we could say that admins have the "ability" to read, write and delete any post.
[CanCanCan](https://github.com/CanCanCommunity/cancancan) and [Pundit](https://github.com/elabs/pundit) are the leaders in this space.  The original gem CanCan (what can? a user do) was written by the creator of RailsCasts if you are a fan!
<p data-visibility='hidden'>View <a href='https://learn.co/lessons/authentication_and_authorization_with_gems'>Authentication And Authorization With Gems</a> on Learn.co and start learning to code for free.</p>
