---
layout: post
title: Custom user model tutorial and django allauth
description: "Customizing the fields given by the default user model and pairing django allauth with it"
category: django
tags: [django, django-allauth, social-accounts, social-login, auth,]
---
Per [this page](https://docs.djangoproject.com/en/dev/topics/auth/customizing/#extending-django-s-default-user) on django docs, if you are entirely happy with django's user model you can just inherit the default user model like below and add any custom fields you need in it. It already has [these fields](https://docs.djangoproject.com/en/dev/ref/contrib/auth/#django.contrib.auth.models.User)

{% highlight python %}
# the models file i.e. users.models 
# I put these customizations in a users app
from django.contrib.auth.models import AbstractUser

# AbstractUser already has the following fields and others.
# username, first_name, last_name
# email, password, groups

class CustomUser(AbstractUser):
    age = models.PositiveIntegerField(null=True, blank=True)
    gender = models.CharField(choices=genders, 
                               default=genders.female, 
                               max_length=20, blank=True)
    # to enforce that you require email field to be associated with
    # every user at registration
    REQUIRED_FIELDS = ["email"]

{% endhighlight %}

Now install this new user model in the settings file
{% highlight python %}
# settings file

########## Custom Auth model
AUTH_USER_MODEL = 'users.CustomUser' # Mind the syntax here. It's <app>.<model>
                                     # not <app>.models.<model>
##########

{% endhighlight %}

This is all you need to do for a custom user model. Now each social account created by the allauth stores an extra data attribute containing the public information shared by the user. If you want to store that info with the user model, you can write a signal receiver for `user_signed_up` signal sent by allauth after registration but *before* login by `allauth`

{% highlight python %}
# users.views
from django.dispatch import receiver
from allauth.account.signals import user_signed_up

@receiver(user_signed_up)
def set_gender(sender, **kwargs):
    user = kwargs.pop('user')
    extra_data = user.socialaccount_set.filter(provider='facebook')[0].extra_data
    gender = extra_data['gender']

    if gender == 'male': # because the default is female.
        user.gender = 'male'

    user.save()

{% endhighlight %}

Similarly, you can use other signals like `user_logged_in`, `pre_social_login` to create some customized workflows
