<script>
    import axios from 'axios';
    import CardComponent from "./components/CardComponent.vue";
    export default {
        name: 'App',
        components: {
            CardComponent
        },
        data() {
            return {
                chatGptAnswer: null, // Store the response from the API
                loading: false, // Optional: Show loading indicator
            };
        },
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
        methods:{
            async getChatGptResponse() {
  this.loading = true;

  const query = "What is the capital of France?";  // Example query

  try {
    const response = await axios.post(
      'https://aiproxy.sanand.workers.dev/openai/v1/chat/completions',
      {
        model: 'gpt-4o-mini',
        messages: [{"role": "user", "content": "What is 2 + 2"}]
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
    this.chatGptAnswer = response.data.choices[0].message.content//.trim();
  } catch (error) {
    console.error('Error fetching data from OpenAI:', error);
    this.chatGptAnswer = "An error occurred while fetching the response.";
  } finally {
    this.loading = false;
  }
}}};
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
        <CardComponent :answer="chatGptAnswer" v-if="chatGptAnswer" />
    </div>
</template>