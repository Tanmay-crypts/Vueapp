<script>
  export default {
    name: "CardComponent",
    props: {
      answer: {
        type: String,
        default: ""
      }
    }
  };
</script>
  
  <style scoped>
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
    <div class="card" v-if="answer">
      <h3>ChatGPT Answer</h3>
      <p>{{ answer }}</p>
    </div>
  </template>
  