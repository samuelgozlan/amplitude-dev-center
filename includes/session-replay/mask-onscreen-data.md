### Mask on-screen data

The Session Replay SDK offers three ways to mask user input, text, and other HTML elements.

| Element           | Description                                                                                                                                                                                                                                               |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<input>`         | Session Replay masks all text input fields by default. When a users enters text into an input field, Session Replay captures asterisks in place of text. To *unmask* a text input, add the class `.amp-unmask`. For example: `<input class="amp-unmask">`. |
| text              | To mask text within non-input elements, add the class `.amp-mask`. For example, `<p class="amp-mask">Text</p>`. When masked, Session Replay captures masked text as a series of asterisks.                                                                 |
| non-text elements | To block a non-text element, add the class `.amp-block`. For example, `<div class="amp-block"></div>`. Session Replay replaces blocked elements with a placeholder of the same dimensions.                                                                |
