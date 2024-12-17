<script setup>
    import axios from 'axios';
    import CardComponent from "./components/CardComponent.vue";
    import { ref ,reactive } from 'vue';
    var k;
var q=` **Interviewer:** Thank you so much for joining us today! We’re excited to hear your thoughts on how we can improve our e-commerce site. Let’s dive right in. Can you tell me a bit about your experience with our site so far?
**Grandma:** Oh, dear, I’d be happy to. I’ve been using your site for quite a while now. It’s quite convenient, and I’ve managed to buy everything from groceries to gifts for my grandchildren. But I think there are a few things that could make it even better for folks like me.
**Interviewer:** That’s great to hear. What features would you like to see added to the site?
**Grandma:** Well, let me think. One thing I’d love is a bigger, clearer font. Sometimes the text is so small that I have to squint to read it. And maybe an option for high-contrast colors would be nice too. I’ve got these old eyes, you see, and it would make things a lot easier if the words were more readable.
**Interviewer:** That sounds like a wonderful idea. Better readability would definitely improve the experience for many users. Are there any other features you’d suggest?
**Grandma:** Oh, absolutely! Another thing I think would be helpful is a simpler checkout process. Sometimes I get confused with all the steps and options. Maybe if there was a big, easy button that said “Check Out” and just took me through it step-by-step, that would be great. 
**Interviewer:** Simplifying the checkout process could definitely make things smoother. What about any specific features for finding items?
**Grandma:** Yes, I think a “favorites” or “wish list” feature would be lovely. I often find things I like, but I’m not always ready to buy them right away. If I could save those items and come back to them later, that would be very helpful. It’d be like having a little shopping list I can keep track of.
**Interviewer:** That’s a fantastic idea. It sounds like it would really help with organizing and planning your purchases. Is there anything else you’d like to see?
**Grandma:** Oh, and a more personal touch would be nice. Maybe something where you could have a chat or a call with a friendly person if you had questions or needed help. Sometimes I’m not so good with technology, and having a little human help could be a real comfort.
**Interviewer:** A personal touch could definitely enhance the shopping experience. We really appreciate these suggestions. How do you think these changes would benefit users like yourself?
**Grandma:** Well, I think it would make shopping a lot more pleasant and less frustrating for people who might have trouble with small print or complex processes. It would make the site feel more welcoming and easier to use. And for me, it’d just be nice to enjoy my shopping without any fuss.
**Interviewer:** Thank you so much for sharing your thoughts. We really value your feedback and will take all these suggestions into consideration. Is there anything else you’d like to add before we wrap up?
**Grandma:** No, I think that’s about it. I’m just happy to help if it means making things better for everyone. Thank you for listening!
**Interviewer:** Thank you, Grandma. Your insights are incredibly valuable, and we’ll work on these ideas to make the site better for all our users. Have a wonderful day!
**Grandma:** You too, dear!
**Grandma:** Well, let me think. One thing I’d love is a bigger, clearer font. Sometimes the text is so small that I have to squint to read it. And maybe an option for high-contrast colors would be nice too. I’ve got these old eyes, you see, and it would make things a lot easier if the words were more readable.

this is first convo . Extract as many user story as possible as a json specified .`


var count=[`create a process/ concept to implement the need/want of user. Later define a usecase for the user with the given benefit/so that.`,`create a ui wireframe for this process`]
var state = reactive({chatGptAnswer: null});
var l=ref(1)
var s=reactive([{"role": "user", "content": `[Case starts]As a language learner, I want an offline mode in the language learning app, so I can continue learning without an internet connection.[case ends] extract me a User Story as json 
  {"role": "A [user role]",
  "need": "[goal]",
  "for": "[benefit]"}`}
]);
    // var  = null;
    
        // methods: {
        //     async getChatGptResponse() {
        //         this.loading = true;

        //         const query =
        //         "What is the capital of France?"; // Example query, you can modify this or make it dynamic

        //         try {
        //             const response = await axios.post(
        //                 //'https://api.openai.com/v1/completions',
        //                 'http://aiproxy.sanand.workers.dev/openai/v1/chat/completions', {
        //                     model: 'gpt-3.5-turbo', // You can use gpt-4 or other models
        //                     prompt: query,
        //                     max_tokens: 50,
        //                     temperature: 0.7
        //                 }, {
        //                     headers: {
        //                         'Authorization': `Bearer eyJhbGciOiJIUzI1NiJ9.eyJlbWFpbCI6IjIyZjMwMDMzMDhAZHMuc3R1ZHkuaWl0bS5hYy5pbiJ9.dtjnpcpwzwPGoItQtJDHcJiF5hDuubsBJH8CDeva6DY`,
        //                         'Content-Type': 'application/json'
        //                     }
        //                 }
        //             );

        //             // Extract the response text
        //             this.chatGptAnswer = response.data.choices[0].text.trim();
        //         } catch (error) {
        //             console.error('Error fetching data from OpenAI:', error);
        //             this.chatGptAnswer = "An error occurred while fetching the response.";
        //         } finally {
        //             this.loading = false;
        //         }
        //     }
        // }
        // export default {
        // name: 'App',
        // components: {
        //     CardComponent
        // },
        // data() {
        //     return {
        //         chatGptAnswer: null, // Store the response from the API
        //         loading: false, // Optional: Show loading indicator
        //     };
        // },
        // methods:{

async function getChatGptResponse(){
  // this.loading = true;
  const query = "What is the capital of France?";  // Example query
  try {
    const response = await axios.post(
      'https://aiproxy.sanand.workers.dev/openai/v1/chat/completions',
      {
        model: 'gpt-4o-mini',
        messages: s
        // max_tokens: 50,
        // temperature: 0.7
      },
      {
        headers: {
          'Authorization': `Bearer eyJhbGciOiJIUzI1NiJ9.eyJlbWFpbCI6IjIyZjMwMDMzMDhAZHMuc3R1ZHkuaWl0bS5hYy5pbiJ9.dtjnpcpwzwPGoItQtJDHcJiF5hDuubsBJH8CDeva6DY`,
          'Content-Type': 'application/json'
        }
      }
    );
    console.log(response);
k=response.data.choices[0].message;
    state.chatGptAnswer = k.content//.trim();
    s.push({"role": k.role, "content": k.content})
    s.push({"role": 'user', "content": count[k]})
    console.log(k);
  } catch (error) {
    console.error('Error fetching data from OpenAI:', error);
    state.chatGptAnswer = "An error occurred while fetching the response.";
  // } finally {
    // this.loading = false;
  }
  // return 0;
}
//}};
</script>

<style>
    button {
        padding: 10px 20px;
        background-color: #42b983;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        
    }
    .outer{
      display: flex;
      align-items: center;
      flex-direction: column;
    }
    button:hover {
        background-color: #366f61;
    }

    .card {
        border: 1px solid #ccc;
        padding: 16px;
        border-radius: 8px;
        width: 300px;
        margin-top: 20px;
        text-align: center;
    }
</style>

<template>
    <div class="outer">
        <button @click="getChatGptResponse">Ask ChatGPT</button>
        <!-- <p>{{ state.chatGptAnswer }}</p> -->
        <CardComponent :answer="state.chatGptAnswer" v-if="state.chatGptAnswer" />
    </div>
</template>