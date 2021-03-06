## API Troubleshooting
If you are using our API and think that something is not working correctly, we will require both the full request and full response from your web developer before we can look into it for you:  

* Full Request - example [here](https://drive.google.com/file/d/0B-baIeSCNY2BcmNFZGZVVWFpbmZDdEhBbUhqMF9MaHdYVl84/view?usp=sharing)
* Full Response - example [here](https://drive.google.com/file/d/0B-baIeSCNY2BdjJ0WFpqaEJiRE8xVDN3VWEwaE1fTkNiTDZ3/view?usp=sharing)

This is so that our tech team can effectively look into the issue for you. Without the above, we will not be able to assist.

## API FAQs

**1. We are creating our own check out and would like to add customer fields eg 'Comments'. How do we include this as part of our check out?**

You will just need to pass the value to the bookings API with the key `custom_field_value`

**2. We are creating our own check out using the Collins API. We know that we have to still take payment through the Collins iFrame. How do we customise the payment page?**

1. Tell us a URL of a stylesheet (that has to be on an HTTPS connection for us to load it) and what you want to use it for (eg app/website)

2. We add this CSS URL to our system for your venue group, with a name eg app

3. When you add the form to your page, you add some code to tell our page which CSS to load, eg

`<script>
  DMN.val('stylesheet', 'app');
  </script>`

4. When the booking form loads, it will also load your CSS so you can override whatever is on the book page. You should add `stylesheet=app` to the end of the URL that you will be sending the user to (to take payment).

**3. We are recording the stages of the booking during live service on our tills. Would it be possible to update the status of the booking in Collins through the API?**

If you have access to our [Bookings Endpoint](http://developers.designmynight.com/api/booking-api/), you will be able to set the stage of a booking. 

To do this, you would need to send a regular POST to update a booking, specifying the `current_stage` field like this:

```
{
  current_stage: 'arrived'
}
```
The possible standard stages that you can set have the following values: 

* `arrived`
* `seated`
* `dessert`
* `bill`
* `left`


**4. We are using the API to look into pre-ordered items. We have set for our pre-order items to have [item customisations](https://collins.uservoice.com/knowledgebase/articles/1806220-collins-pre-orders-adding-diet-types-allergies) within Collins. How do these customisations display in the API response?**

Here is an example of a pre-order with a single item that has a single option added:

```
{
  "id": "5b5de8873806c8176564bc82",
  "created_date": "2018-07-29T17:17:11",
  "name": "Joe McBurger",
  "email": "joemcg@example.com",
  "items": [
    {
      "id": "5b224eb9f366247fd128537c",
      "menu_id": "5b224a75b22f5950761cd374",
      "name": "Eggs Royale",
      "quantity": 1,
      "total": 12,
      "type": "food",
      "sub_type": "brunch",
      "options": [
        {
          "label": "Large",
          "values": [
            {
              "label": "Large",
              "price_change": 5
            }
          ]
        }
      ],
      "price": 12,
      "base_price": 7,
      "options_price": 5,
      "options_string": "Large",
      "for_name": "Joe",
      "discount_value": 0
    }
  ],
  "total_cost": 12,
  "amount_paid": 0,
  "source": "customer",
  "status": "complete",
  "service_charge_percentage": 0,
  "service_charge_amount": 0,
  "total_discount": 0
}
```

The `label` and `options_string` refer to the customisation of the pre-order item.
 
