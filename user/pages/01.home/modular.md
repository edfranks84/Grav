---
title: One Page Demo Site
menu: Home
cache_enable: false
onpage_menu: false
heading: Stay Informed With Our Newsletter
form:
    name: my-nice-form
    action: /home
    fields:
        - name: email
          id: email
          classes: form-control form-control-lg
          label: Email
          placeholder: Enter your email address
          type: text
          validate:
            rule: email
            required: true

    buttons:
        - type: submit
          value: Send
          class: button button-solid blue

    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.from }}"
              - "{{ form.value.email }}"
            subject: "[Feedback] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Thank you for your feedback!
        - display: thankyou    

content:
    items: '@self.modular'
    order:
        by: default
        dir: asc
        custom:
            - _hero
            - _history
            - _latestnews
            - _why
            - _portfolio
            - _contact

---

