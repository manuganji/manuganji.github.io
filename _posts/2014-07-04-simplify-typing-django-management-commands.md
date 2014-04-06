---
layout: post
title: Simplify typing django management commands
description: "Using virtualenvwrapper's postactivate and postdeactive, add some helpful commands to your shell"
category: django, productivity
tags: [django, code, productivity]
---
Virtualenv postactivate and postdeactivate files for django.
Place these files at `$VIRTUAL_ENV/bin`. That is inside the `bin` folder inside the `virtualenv` directory.

Because it quickly gets problematic to type `python manage.py <command>` in the terminal. It's even more difficult if your project uses multiple `manage.py` files. It's also quite convenient to not have to type the whole `python manage.py schemamigration <app_name> --auto` everytime.
<script src="https://gist.github.com/manuganji/9069466.js"></script>
