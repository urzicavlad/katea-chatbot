<script>
  import SendIcon from "./SendIcon.svelte";
  import { messages } from "../stores/messages.js";
  let active = false;
  let text = "";
  export let placeholder = "Scrie aici mesajul";

  const submitText = ev => {
    ev.preventDefault();
    messages.set([
      ...$messages,
      {
        type: "text",
        author: "user",
        text
      }
    ]);
    text = "";
  };
  const handleKey = event => {
    if (event.keyCode === 13 && !event.shiftKey) {
      submitText(event);
    }
  };
</script>

<style>
  .sc-user-input {
    min-height: 55px;
    margin: 0px;
    position: relative;
    bottom: 0;
    display: flex;
    background-color: #f4f7f9;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    transition: background-color 0.2s ease, box-shadow 0.2s ease;
  }

  .sc-user-input--text {
    width: 300px;
    resize: none;
    border: none;
    outline: none;
    border-bottom-left-radius: 10px;
    box-sizing: border-box;
    padding: 18px;
    font-size: 15px;
    font-weight: 400;
    line-height: 1.33;
    white-space: pre-wrap;
    word-wrap: break-word;
    color: #565867;
    -webkit-font-smoothing: antialiased;
    max-height: 200px;
    overflow: scroll;
    bottom: 0;
    overflow-x: hidden;
    overflow-y: auto;
  }

  .sc-user-input--text:empty:before {
    content: attr(placeholder);
    display: block; /* For Firefox */
    color: rgba(86, 88, 103, 0.3);
    outline: none;
  }

  .sc-user-input--buttons {
    width: 50px;
    position: absolute;
    right: 30px;
    height: 100%;
    display: flex;
  }

  .sc-user-input--button:first-of-type {
    width: 40px;
  }

  .sc-user-input--button {
    width: 30px;
    height: 55px;
    padding-left: 3px;
    padding-right: 3px;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .sc-user-input.active {
    box-shadow: none;
    background-color: white;
    box-shadow: 0px -5px 20px 0px rgba(150, 165, 190, 0.2);
  }

  .sc-user-input--file-icon {
    height: 20px;
    width: 20px;
    cursor: pointer;
    align-self: center;
    outline: none;
  }

  .sc-user-input--button label {
    position: relative;
    height: 24px;
    padding-left: 3px;
    cursor: pointer;
  }

  .sc-user-input--button label:hover path {
    fill: rgba(86, 88, 103, 1);
  }

  .sc-user-input--button input {
    position: absolute;
    left: 0;
    width: 100%;
    z-index: 99999;
    height: 100%;
    opacity: 0;
    cursor: pointer;
    overflow: hidden;
  }

  .file-container {
    background-color: #f4f7f9;
    border-top-left-radius: 10px;
    padding: 5px 20px;
    color: #565867;
  }

  .delete-file-message {
    font-style: normal;
    float: right;
    cursor: pointer;
    color: #c8cad0;
  }

  .delete-file-message:hover {
    color: #5d5e6d;
  }

  .delete-message {
    font-style: normal;
    font-size: 10px;
    line-height: 16px;
    position: absolute;
    top: -5px;
    width: 16px;
    height: 16px;
    padding: 0;
    margin: 0;
    right: -5px;
    cursor: pointer;
    color: #fff;
    background: #4e8cff;
    border: 0;
    border-radius: 50%;
  }

  .delete-message:hover {
    color: #c8cad0;
  }

  .delete-message:focus,
  .delete-message:active {
    border: 0;
    outline: 0;
  }

  .icon-file-message {
    margin-right: 5px;
  }

  .sc-user-input--emoji-icon-wrapper,
  .sc-user-input--file-icon-wrapper {
    background: none;
    border: none;
    padding: 0px;
    margin: 0px;
    outline: none;
  }

  .sc-user-input--emoji-icon-wrapper:focus {
    outline: none;
  }

  .sc-user-input--emoji-icon {
    height: 18px;
    cursor: pointer;
    align-self: center;
  }

  .sc-user-input--emoji-icon path,
  .sc-user-input--emoji-icon circle {
    fill: rgba(86, 88, 103, 0.3);
  }

  .sc-user-input--emoji-icon-wrapper:focus .sc-user-input--emoji-icon path,
  .sc-user-input--emoji-icon-wrapper:focus .sc-user-input--emoji-icon circle,
  .sc-user-input--emoji-icon.active path,
  .sc-user-input--emoji-icon.active circle,
  .sc-user-input--emoji-icon:hover path,
  .sc-user-input--emoji-icon:hover circle {
    fill: rgba(86, 88, 103, 1);
  }
</style>

<div>
  <form class="sc-user-input" class:active>
    <div
      role="button"
      tabIndex="0"
      on:focus={e => {
        active = true;
      }}
      on:blur={e => {
        active = false;
      }}
      bind:textContent={text}
      on:keydown={handleKey}
      contenteditable="true"
      {placeholder}
      class="sc-user-input--text" />
    <div class="sc-user-input--buttons">
      <div class="sc-user-input--button">
        <SendIcon onClick={submitText} />
      </div>
    </div>
  </form>
</div>
