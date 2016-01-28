# Authentication/Authorization with Gems

## Learning Objectives

  1. Understand the landscape of gems that can be used to do authorization and authentication in Rails.

## Overview

In the first half of this unit we learned how to roll our own authentication scheme.  Authentication deals with verifying WHO a user is.  In the second half of this unit we're also going to learn how to do authorization.  Authorization deals with WHAT a user is allowed to do once we know WHO they are.  

Most security professionals will tell you NEVER to roll your own authentication logic as we did in the first half of the unit.  This is because as a young (or even experienced programmer) it's unlikely you are a match for the myriad of tricks hackers are going to use to try and hack into your site.  Forget to salt your passwords?  You're open to rainbow table attacks.  Use the wrong hashing algorithm?  You're open to brute force attacks.  Leave security to those who are experts at it!

There are two solutions to this problem.  One, which we've already learned is letting someone else take care of logging users in!  Rather than devoting your scare resources to solving a solved problem, let one of the internet giants like Facebook deal with authentication by leveraging the oauth protocol.  If Facebook gets hacked, you probably wouldn't have been safer implementing your own authentication scheme...

Along the same lines as this solution, is leveraging the Rails communities open source nature and using a battle tested gem to implement authentication.  In the same way using the omniauth gem can help you avoid implementing the oauth specification correctly yourself, there are a host of gems the Rails community has built over the years to help you avoid implementing authentication and authorization yourself.

One of the gems everybody loves almost as much as they hate it is Devise.  It's without a doubt the leader in the authentication space, and has over 3,000 commits in it's 7 year history.  It's heavily metaprogrammed, modularized and has a solution to just about any need your authentication scheme might require.  Our biggest complaint with devise is that it often obscures what's going on due to its metaprogramming, which makes it hard to change if it's configuration options don't account for EXACTLY your use case.  The great thing about Devise is it also offers some authorization options as well.

Other gems worth looking at in this space are [Warden](https://github.com/hassox/warden) (which devise is based around) and [Authlogic](https://github.com/binarylogic/authlogic)

## Authorization

Authorization deals with WHAT a user is allowed to do, once we know WHO that user is.  Can this particular user delete a post?  Can they view posts written by other users?  Authorization helps you answer these questions.

Although Devise doesn't have out of the box support for authorization, it's common to implement "roles" using Devise.  Roles allow us to segment our users into types or kinds of users.  For example, admins, teachers, and students.  By leveraging ActiveRecord's enum feature, you can define a user as having a specific role.  If you have simple enough authorization requirements this might be enough.  However, if your roles get more complicated you might want to bring in another gem to do the heavy lifting. [Rolify](https://github.com/RolifyCommunity/rolify)

You can pair the concept of roles with other gems that allow you to specify what "abilities" or "policies" users or types of users.  For example we could say that admins have the "ability" to read, write and delete any post.
[CanCanCan](https://github.com/CanCanCommunity/cancancan) and [Pundit](https://github.com/elabs/pundit) are the leaders in this space.  The original gem CanCan (what can? a user do) was written by the creator of RailsCasts if you are a fan!