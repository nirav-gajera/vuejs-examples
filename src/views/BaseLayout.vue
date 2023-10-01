<template>
    <div class="container">
      <header>
        <slot name="header"></slot>
      </header>
      <main>
        <slot name="default1"></slot>
      </main>
      <footer>
        <slot name="footer"></slot>
      </footer>
      <button class="fancy-btn">
  	<slot/> <!-- slot outlet -->
	</button>
    </div>
  
  </template>
  
  <style>
    footer {
      border-top: 1px solid #ccc;
      color: #666;
      font-size: 0.8em;
    }
    .fancy-btn {
        color: #fff;
        background: linear-gradient(315deg, #42d392 25%, #647eff);
        border: none;
        padding: 5px 10px;
        margin: 5px;
        border-radius: 8px;
        cursor: pointer;
    }
  </style>