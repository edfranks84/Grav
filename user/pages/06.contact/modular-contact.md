---
title: Contact
cache_enable: false
heading: Stay Informed With Our Newsletter
form:
    name: my-nice-form
    action: /contact
    fields:
        - name: Name
          id: Name
          label: Name
          placeholder: Enter your name
          type: text
          validate:
            required: true
        - name: email
          id: email
          label: Email
          placeholder: Enter your email address
          type: text
          validate:
            rule: email
            required: true 
        - name: Message
          id: Message
          label: Message
          placeholder: Your message
          type: textarea
          validate:
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
            - _contact-hero
            - _contact-info
            - _contact-form

---

