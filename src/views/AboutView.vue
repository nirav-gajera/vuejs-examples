<!-- eslint-disable vue/require-v-for-key -->
<script setup>
import { ref } from 'vue'
const count = ref(0)


import { reactive, computed } from 'vue'

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

// a computed ref
const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})

//v-if v-else
const awesome = ref(true)

//v-for
const items = ref([{ message: 'foo' }, { message: 'bar' }])

//Displaying Filtered/Sorted Results
const numbers = ref([1, 2, 3, 4, 5, 6])

const evenNumbers = computed(() => {
  return numbers.value.filter((n) => n % 2 === 0)
})


const name = ref('Vue.js')

//method handler
function greet(event) {
  alert(`Hello ${name.value}!`)
  // `event` is the native DOM event
  if (event) {
    alert(event.target.tagName)
  }
}

//event argument inline handler
function warn(message, event) {
  if (event) {
    event.preventDefault()
  }
  alert(message)
}

//form input binding
const message = ref('')

//multiline
const message2 = ref('')

//checkbox
const checked = ref(true)

//checkbox multiple
const checkedNames = ref([])

//radio
const picked = ref('One')

//select single
const selected = ref('')

//selecte multiple
const selected2 = ref([])

//template refs
import { onMounted } from 'vue'

const list = ref([1, 2, 3])

const itemRefs = ref([])

onMounted(() => {
  // alert(itemRefs.value.map(i => i.textContent))
  console.log(itemRefs.value.map(i => i.textContent))

})

//passing pops
import BlogPost from './BlogPost.vue'
  
const posts = ref([
  { id: 1, title: 'My journey with Vue' },
  { id: 2, title: 'Blogging with Vue' },
  { id: 3, title: 'Why Vue is so fun' }
])
const postFontSize = ref(1)

// alert box
import AlertBox from './AlertBox.vue'

//Event Arguments
function increaseCount(n) {
  count.value += n
}

// Multiple v-model bindings
import UserName from './UserName.vue'

const first = ref('Nirav')
const last = ref('Gajera')

//slots 
import BaseLayout from './BaseLayout.vue'

//scoped slots
import FancyList from './FancyList.vue'

// Renderless Components
import MouseTracker from './MouseTracker.vue'

// Async State
import { useFetch } from './useFetch.js'

const baseUrl = 'https://jsonplaceholder.typicode.com/todos/'
const id = ref('1')
const url = computed(() => baseUrl + id.value)

const { data, error, retry } = useFetch(url)

// Define the plugin
// eslint-disable-next-line no-unused-vars
const myPlugin = {
  install(app) {
    // Add a global method or property
    app.config.globalProperties.$myAlert = showAlert;
  }
};

// Use the plugin
const showAlert = () => {
  alert('This is a custom plugin alert!');
};



</script>

<template>
  <div class="container" style="max-width: 600px">
 
    <div class="about">
      <h1>This is an about page</h1>
    </div>
    <hr>
    <h4><i class="fa fa-check"></i> Button Counter example(inline handler) :</h4>
    <button @click="count++" class="btn btn-sm btn-primary" style="font-weight: bold; ">Click here </button>
    <p>Count is: {{ count }}</p> 
    <hr>
    <h4><i class="fa fa-check"></i> a computed ref example :</h4>
    <p>Has published books:
      <code>{{ publishedBooksMessage }}</code>
    </p>
    <hr>
    <h4><i class="fa fa-check"></i> v-if v-else example : </h4>
    <h6>(click Toggle button)</h6><br>
    <button @click="awesome = !awesome" class="btn btn-sm btn-outline-warning" style="font-weight: bold;">Toggle </button>

    <span style="margin-left: 10px;">
      <h4 v-if="awesome"><i>Vue is awesome!</i></h4>
      <h4 v-else><b style="font-family: cursive; color: rgb(207, 32, 32);">Laravel is cool </b></h4>
    </span>

    <hr>
    <h4><i class="fa fa-check"></i> v-for example :</h4>
    <ol>
      <!-- eslint-disable-next-line vue/require-v-for-key -->
      <li v-for="item in items">
        {{ item.message }}
      </li>
    </ol>
    <hr>

    <h4><i class="fa fa-check"></i> Displaying Filtered/Sorted Results :</h4>
    <ul>
      <!--  eslint-disable-next-line vue/require-v-for-key -->
      <li v-for="n in evenNumbers">{{ n }}</li>
    </ul>
    
    <hr>
    <!-- `greet` is the name of the method defined above -->
    <h4><i class="fa fa-check"></i> Method Handler Example :</h4>
    <h6>(click Greet button)</h6><br>
    <button @click="greet" class="btn btn-sm btn-info" style="font-weight: bold;">Greet</button>
    <hr>

    <h4><i class="fa fa-check"></i> Accesing event argument in inline Handlers: </h4>
    <!-- using $event  special variable -->
    <button @click="warn('Form cannot be submmited yet.', $event)" class="btn btn-sm btn-secondary">Submit </button>
    &nbsp;
    <!-- using inline arrow function -->
    <button @click="(event) => warn('form cannot be submmited yet', $event)" class="btn btn-sm btn-outline-secondary"
      value="using inline arrow function">Submit </button>
    <hr>

    <!-- Form input binding -->
    <h4><i class="fa fa-check"></i> Form input binding(text):</h4>
    <p>Message is: {{ message }}</p>
  <input v-model="message" placeholder="edit me" />
  <br>
  <br>
  <h4><i class="fa fa-check"></i> Multiline text:</h4>
  <span>Multiline message is:</span>
<p style="white-space: pre-line;">{{ message2 }}</p>
<textarea v-model="message2" placeholder="add multiple lines"></textarea>
<hr>

<h4><i class="fa fa-check"></i> Checkbox:</h4>
<input type="checkbox" id="checkbox" v-model="checked" />
	<label for="checkbox">{{ checked }}</label>
  <h4><i class="fa fa-check"></i> Multiple checkbox:</h4>
  <div>Checked names: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames" />
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
<label for="mike">Mike</label>
<hr>

<h4><i class="fa fa-check"></i> Radio: </h4>
<div>Picked: {{ picked }}</div>

	<input type="radio" id="one" value="One" v-model="picked" />
	<label for="one">One</label> &nbsp;

	<input type="radio" id="two" value="Two" v-model="picked" />
  <label for="two">Two</label>
  <hr>
  
  <h4><i class="fa fa-check"></i> Select(single):</h4>
  <span> Selected: &nbsp; {{ selected }}</span>

  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <br>
  <br>
  <h4><i class="fa fa-check"></i> Select(multiple):</h4>
  <div>Selected: {{ selected2 }}</div>

<select v-model="selected2" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<hr>
<!-- template referance -->
<h4><i class="fa fa-check"></i> Template Refs: </h4>
 <ul>
    <!-- eslint-disable-next-line vue/require-v-for-key -->
    <li v-for="item in list" ref="itemRefs">
      {{ item }}
    </li>
  </ul>
<hr>
<!-- passign props -->
<h4><i class="fa fa-check"></i> Passing pops: </h4>
<div :style="{ fontSize: postFontSize + 'em' }">
    <BlogPost
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      @enlarge-text="postFontSize += 0.1"
    ></BlogPost> 
    </div>
    <hr>

    <!-- alert box -->
    <h4> <i class="fa fa-warning"></i> Alert box</h4>
    <AlertBox>
  	Something bad happened.
	</AlertBox>
   
  <hr>
<!-- Event Arguments -->
<MyButton @increase-by="increaseCount" />

<!--  Multiple v-model bindings -->
<h4><i class="fa fa-check"></i> Multiple v-model bindings: </h4>

<h5>{{ first }} {{ last }}</h5>
  <UserName
    v-model:first-name="first"
    v-model:last-name="last"
  />
  <hr>
<!--slot  -->
<h4><i class="fa fa-check"></i> Slots Example</h4>
<BaseLayout>
    <template #header>
      <h5>Here might be a page title</h5>
    </template>

    <template #default1>
      <p>A paragraph for the main content.</p>
      <p>And another one.</p>
    </template>

    <template #footer>
      <p>Here's some contact info</p>
    </template>
    <FancyButton>
    Click me <!-- slot content -->
 	</FancyButton>
  </BaseLayout>
<hr>
  <!-- scoped slots -->
  <h4> <i class="fa fa-check"></i> Fancy list(Scoped slot example) </h4>
  <FancyList :api-url="url" :per-page="10">
    <template #item="{ body, username, likes }">
      <div class="item">
        <p>{{ body }}</p>
        <p class="meta">by {{ username }} | {{ likes }} likes</p>
      </div>
    </template>
  </FancyList>
  <hr>
  <!-- Renderless Components -->
  <h4><i class="fa fa-check"></i> Mouse tracker(Renderless Components ex)</h4>
  <MouseTracker v-slot="{ x, y }">
  	Mouse is at: {{ x }}, {{ y }}
	</MouseTracker>
    <hr>

    <!-- Async State -->
    <h4><i class="fa fa-check"></i> Async State Example </h4>
    Load post id:
      <!-- eslint-disable-next-line vue/require-v-for-key -->
  <button v-for="i in 5" @click="id = i">{{ i }}</button>

	<div v-if="error">
    <p>Oops! Error encountered: {{ error.message }}</p>
    <button @click="retry">Retry</button>
  </div>
  <div v-else-if="data">Data loaded: <pre>{{ data }}</pre></div>
  <div v-else>Loading...</div>
<hr>

<!-- Plugin  -->
<h4><i class="fa fa-check"></i> Plugin Example</h4>
    <button @click="showAlert">Show Alert</button>
<hr>


  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 50vh;
    display: flex;
    align-items: center;
    margin-top: -150px;
  }
}

span {
  display: inline-block;
  vertical-align: middle;
  margin-top: 5px;
}

hr {
  border: solid black;

}
select[multiple] {
  width: 100px;
}
.meta {
  font-size: 0.8em;
  color: #42b883;
}
</style>
