:::(Error) ()
There is currently an issue when using giftcards with Payolution. Our team is developing a fix for it.
:::

## Prerequisites
Before proceeding with the integration, make sure you have [installed and configured](https://documentation.spryker.com/docs/payolution-configuration) the Payolution module.

## Frontend Integration
To show Payolution on Frontend, extend the payment view:

**src/Pyz/Yves/CheckoutPage/Theme/default/views/payment/payment.twig**

 ```php
 {% extends template('page-layout-checkout', 'CheckoutPage') %}

{% define data = {
    backUrl: _view.previousStepUrl,
    forms: {
        payment: _view.paymentForm
    },
    title: 'checkout.step.payment.title' | trans,
    customForms: {}
} %}

{% block content %}
    {% embed molecule('form') with {
        class: 'box',
        data: {
            form: data.forms.payment,
            options: {
                attr: {
                    id: 'payment-form'
                }
            },
            submit: {
                enable: true,
                text: 'checkout.step.summary' | trans
            },
            cancel: {
                enable: true,
                url: data.backUrl,
                text: 'general.back.button' | trans
            },
            customForms: data.customForms
        }
    } only %}
        {% block fieldset %}
            {% for name, choices in data.form.paymentSelection.vars.choices %}
                {% set paymentProviderIndex = loop.index0 %}
                <h5>{{ ('checkout.payment.provider.' ~ name) | trans }}</h5>
                <ul>
                    {% for key, choice in choices %}
                        <li class="list__item spacing-y clear">
                            {% embed molecule('form') with {
                                data: {
                                    form: data.form[data.form.paymentSelection[key].vars.value],
                                    enableStart: false,
                                    enableEnd: false,
                                    customForms: data.customForms
                                },
                                embed: {
                                    index: loop.index ~ '-' ~ paymentProviderIndex,
                                    toggler: data.form.paymentSelection[key]
                                }
                            } only %}
                                {% block fieldset %}
                                    {{ form_row(embed.toggler, {
                                        required: false,
                                        component: molecule('toggler-radio'),
                                        attributes: {
                                            'target-class-name': 'js-payment-method-' ~ embed.index,
                                        }
                                    }) }}
                                    {% set templateName = data.form.vars.template_path | replace('/', '-') %}
                                    {% set viewName = data.form.vars.template_path | split('/') %}

                                    <div class="col col--sm-12 is-hidden js-payment-method-{{embed.index}}">
                                        <div class="col col--sm-12 col--md-6">
                                            {% if 'Payolution' in data.form.vars.template_path %}
                                                {% include view(viewName[1], viewName[0]) with {
                                                    form: data.form.parent
                                                } only %}
                                            {% else %}
                                                {{ parent() }}
                                            {% endif %}
                                        </div>
                                    </div>
                                {% endblock %}
                            {% endembed %}
                        </li>
                    {% endfor %}
                </ul>
            {% endfor %}
        {% endblock %}
    {% endembed %}
{% endblock %}

```