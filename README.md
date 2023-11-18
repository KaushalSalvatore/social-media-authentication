### Social Media Authentication

#### this is Django web application with social media authentication like gmail ,facebook ,github 

#### Required Installation for Authentication 

- [All Auth Doc](https://docs.allauth.org/en/latest/introduction/index.html#)

- [Requirements](https://docs.allauth.org/en/latest/installation/requirements.html)

- [Quickstart Steps](https://docs.allauth.org/en/latest/installation/quickstart.htm)

- [Google Login](https://docs.allauth.org/en/latest/socialaccount/providers/google.html)

- [Facebook Login](https://docs.allauth.org/en/latest/socialaccount/providers/facebook.html)

- [GitHub](https://docs.allauth.org/en/latest/socialaccount/providers/github.html)

#### install Packages 

```bash
pip install django-allauth
```

```bash
pip install django-crispy-forms
```

```bash

```

#### Add the following to the settings.py in projet

```bash
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                # Already defined Django-related contexts here

                # `allauth` needs this from django
                'django.template.context_processors.request',
            ],
        },
    },
]
```

```bash
AUTHENTICATION_BACKENDS = [
    # Needed to login by username in Django admin, regardless of `allauth`
    'django.contrib.auth.backends.ModelBackend',

    # `allauth` specific authentication methods, such as login by email
    'allauth.account.auth_backends.AuthenticationBackend',
]
```

```bash
INSTALLED_APPS = [
     # The following apps are required:
    'django.contrib.auth',
    'django.contrib.messages',

    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google',
    'allauth.socialaccount.providers.facebook',
    'allauth.socialaccount.providers.github',
]
```

```bash
MIDDLEWARE = [
     # Add the account middleware:
    "allauth.account.middleware.AccountMiddleware",
]
```

```bash
SOCIALACCOUNT_PROVIDERS = {
    'google': {
        'SCOPE': [
            'profile',
            'email',
        ],
        'AUTH_PARAMS': {
            'access_type': 'online',
        },
        'OAUTH_PKCE_ENABLED': True,
    }
},
 'facebook': {
        'METHOD': 'oauth2',  # Set to 'js_sdk' to use the Facebook connect SDK
        'SDK_URL': '//connect.facebook.net/{locale}/sdk.js',
        'SCOPE': ['email', 'public_profile'],
        'AUTH_PARAMS': {'auth_type': 'reauthenticate'},
        'INIT_PARAMS': {'cookie': True},
        'FIELDS': [
            'id',
            'first_name',
            'last_name',
            'middle_name',
            'name',
            'name_format',
            'picture',
            'short_name'
        ],
        'EXCHANGE_TOKEN': True,
        'LOCALE_FUNC': 'path.to.callable',
        'VERIFIED_EMAIL': False,
        'VERSION': 'v13.0',
        'GRAPH_API_URL': 'https://graph.facebook.com/v13.0',
    },
    'github': {
        'SCOPE': [
            'user',
            'repo',
            'read:org',
        ],
    }
```

```bash
INSTALLED_APPS = [
        'crispy_forms'
]
```

####  Add this in project file urls.py

```bash
urlpatterns = [
    path('accounts/', include('allauth.urls')),
]
```