---
layout: post
title:      "Helper Methods & how they helped with my Sinatra Project."
date:       2020-10-26 19:01:24 -0400
permalink:  helper_methods_-_how_they_helped_with_my_sinatra_project
---


For my Sinatra Portfolio Project I created a simple CRUD app called Post Your Positivity. During my first assessment for my CLI project, I realized that my code wasn’t very DRY so I knew that I wanted to keep that in mind when creating this project. To make my application more DRY I decided to implement multiple helper methods.
> “A helper method is a term used to describe some method that is reused often by other methods or parts of a program. Helper methods are typically not too complex and help shorten code for frequently used minor tasks. Using helper methods can also help to reduce error in code by having the logic in one place.”(Code Academy)

1st helper method: Checks to see if we logged anyone in - have we added a user id key with the users database id to the session hash
```
def current_user 
      @current_user ||= User.find_by(id: session[:user_id])
    end

```

2nd helper method: Checks to see if any user is logged in - returns a boolean true or false based on if there is a current user
```
def logged_in? 
      !!current_user
    end

```

3rd helper method: checks to see that the positive post belongs to the current user
```
def authorized_to_edit?(positive_post)
      positive_post.user == current_user
  end

```
4th helper method: Redirects a user to the homepage if they are not logged in
```
def redirect_if_not_logged_in
      if !logged_in?
        flash[:errors] = "You must be logged in view that page"
        redirect '/'
      end
    end
```

5th helper method: finds the positive post
```
def set_positive_post
        @positive_post = PositivePost.find(params[:id])
    end
```

