# Stimulus Stripe Elements controller

A Stimulus controller to use Stripe.js and Elements

## Install

Assuming [StimulusJS](https://stimulusjs.org) is already installed. Add the `stimulus-stripe-elements` module:

```bash
$ yarn add stimulus-stripe-elements
```

or

```bash
$ npm install stimulus-stripe-elements
```

Next, include the stripe.js script on your pages.
```html
<head>
<script src="https://js.stripe.com/v3/"></script>
</head>
```

### HTML
```html
<form
  data-controller="stripe"
  data-target="stripe.form"
  data-action="stripe#submit"
  data-stripe-public-key="{stripe_public_key}"
  data-stripe-style="
    "base": {
      "fontFamiliy": "system-ui",
      "fontSize": "16px",
      "color": "#3d4852",
      "fontSmoothing": "antialiased",
      "::placeholder": {
        "color": "#CFD7DF"
      },
      "invalid": {
        "color": "#e5424d",
        ":focus": {
          "color": "#303238"
        }
      }
    }
  "
  action="" method="post">
  <div class="field">
    <label for="card-element">Credit or debit card</label>
    <div data-target="stripe.card" data-action="change->stripe#change" class="input">
    <div data-target="stripe.errors" role="alert"></div>
  </div>

  <button name="button" type="submit" class="btn btn--primary">Submit payment</button>
</form>

```
### ERB
```erb
<%= form_with(
  url: billing_url,
  local: true,
  data: {
    controller: "stripe",
    target: "stripe.form",
    action: "stripe#submit",
    stripe_public_key: Rails.application.credentials.dig(Rails.env.to_sym, :stripe, :public_key),
    stripe_style: '{
      "base": {
        "fontFamiliy": "system-ui",
        "fontSize": "16px",
        "color": "#3d4852",
        "fontSmoothing": "antialiased",
        "::placeholder": {
          "color": "#CFD7DF"
        },
        "invalid": {
          "color": "#e5424d",
          ":focus": {
            "color": "#303238"
          }
        }
      }
    }'
  }) do |form| %>

  <div class="field">
    <label for="card-element">Credit or debit card</label>
    <div data-target="stripe.card" data-action="change->stripe#change" class="input"> </div>
    <div data-target="stripe.errors" role="alert"></div>
  </div>

  <%= form.button "Submit payment", class: "btn btn--primary", data: { disable_with: "Submitting payment…" } %>
<% end %>
```

## Contributing

Bug reports and pull requests are welcome on GitHub at <https://github.com/eelcoj/stimulus-stripe-elements>.

## License

This package is available as open source under the terms of the MIT License.
