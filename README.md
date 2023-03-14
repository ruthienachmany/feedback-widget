# NJ Feedback widget

A generic, reusable [web component](https://developer.mozilla.org/en-US/docs/Web/Web_Components) that can be added to any New Jersey page to get quick, in-page feedback from the user. This is inspired by the [CA Design System's similar component](https://designsystem.webstandards.ca.gov/components/page-feedback/readme/). It is mobile-responsive, accessible (tested with [axe](https://www.deque.com/axe/) tool), and supports English and Spanish language.

## How to use it

1. Download the `feedback-widget.js` file. This is the only file you need.
2. In your own page's HTML, load the JS file so that you can use the component. The `defer` attribute is to wait until the page content is parsed before loading the JS, since this is not an essential element.

```javascript
<script src="feedback-widget.js" defer></script>
```

3. Add the following tags to your page's HTML code, wherever you want to place the component, most likely at the bottom of a page. It's just like using any other HTML tag.

```html
<feedback-widget></feedback-widget>
```

## How it works

When the user interacts with the feedback widget, our Feedback API (https://github.com/newjersey/feedback-api) will then add data (see below) to our Google Sheets database, which can then be visualized in Looker Studio.

### User flow

1. Widget will ask user if they found what they were looking for on page. User can select "Yes" or "No". (Data recorded: page URL, time of interaction, and Yes/No selection)
2. Widget will ask user if they want to share an open-ended feedback. User can submit freeform text. (Data recorded: submitted comment)
3. Widget will ask user if they want to share their email to join a user testing group. User can submit email address. (Data recorded: email address)
4. Widget will thank user for sharing

### Multi-language support

The component supports English and Spanish content and switching between the two. If you'd like to switch the language of the component's content, use JavaScript to send a custom event using the code below. For example, we can send this event in a click handler for a button.

```javascript
document.getElementById("languageButton").addEventListener("click", (e) => {
  const customEvent = new CustomEvent("changeLanguage", {
    detail: "es" /* "en" for English or "es" for Spanish */,
    bubbles: true,
  });
  e.target.dispatchEvent(customEvent);
});
```

## Where it's used

- NJ DOL, MyLeaveBenefits, Maternity Timeline Tool (Welcome) - https://nj.gov/labor/myleavebenefits/worker/maternity/timeline-welcome.shtml
- NJ DOL, MyLeaveBenefits, Maternity Timeline Tool (Tool) - https://nj.gov/labor/myleavebenefits/worker/maternity/timeline-tool.shtml
- NJ DOL, MyLeaveBenefits, What happens after I apply? - https://nj.gov/labor/myleavebenefits/worker/resources/claims-status.shtml
- NJ DOL, MyLeaveBenefits, Announcing a new way to log in - https://www.nj.gov/labor/myleavebenefits/worker/resources/login-update.shtml
- NJ DOL, UI Claim Status - https://uistatus.dol.state.nj.us/
