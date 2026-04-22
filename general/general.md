# General Snippets that helps
## Javascript Snippets
### Link shower
This shows the href value of links while making links visible all through out the page.

```js
// Replace 'target-class' with the class name of your div
const container = document.querySelector('.site');

if (container) {
  const links = container.querySelectorAll('a');

  links.forEach(link => {
    // Highlight with a 3px dashed border
    link.style.border = '1px dashed green';
    link.style.padding = '2px';

	const hrefValue = link.getAttribute('href');

    // Create a label showing the href beside the link
    const hrefLabel = document.createElement('span');
    hrefLabel.textContent = ` [${hrefValue}]`;
    hrefLabel.style.color = 'blue';
    hrefLabel.style.fontSize = 'smaller';
    hrefLabel.style.marginLeft = '4px';

    // Insert the label right after the link
    link.insertAdjacentElement('afterend', hrefLabel);
  });
} else {
  console.warn('No container found with the specified class.');
}
```