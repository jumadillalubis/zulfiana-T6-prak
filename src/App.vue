<template>
  <div>
    <form @submit.prevent="save">
      <input type="text" v-model="form.title" placeholder="Title" class="input-field" /><br />
      <textarea v-model="form.content" placeholder="Content" class="input-field"></textarea><br />
      <button type="submit" class="btn">{{ form.id ? 'Update' : 'Save' }}</button>
    </form>
    <ul>
      <li v-for="article in articles" :key="article.id">
        <div class="article">
          <h3>{{ article.title }}</h3>
          <p>{{ article.content }}</p>
          <div class="btn-group">
            <button @click="edit(article)" class="edit-btn">Edit</button>
            <button @click="remove(article.id)" class="delete-btn">Delete</button>
          </div>
        </div>
      </li>
    </ul>
    <button @click="load" class="btn load-btn">Load</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articles: [],
      form: {
        id: null,
        title: '',
        content: ''
      }
    };
  },
  methods: {
    save() {
      if (this.form.id) {
        // Update existing article
        const index = this.articles.findIndex(article => article.id === this.form.id);
        if (index !== -1) {
          this.articles.splice(index, 1, { ...this.form });
        }
      } else {
        // Add new article
        const newArticle = { ...this.form, id: Date.now().toString() };
        this.articles.push(newArticle);
      }
      this.resetForm();
    },
    edit(article) {
      this.form = { ...article };
    },
    remove(id) {
      const index = this.articles.findIndex(article => article.id === id);
      if (index !== -1) {
        this.articles.splice(index, 1);
      }
    },
    load() {
      // Here we simulate loading data, replace with actual data fetching
      this.articles = [
        { id: '1', title: 'judul', content: 'Ini Content' },
        { id: '2', title: 'judul 2', content: 'Ini Content 2' },
        { id: '3', title: 'judul 3', content: 'Ini Content 3' }
      ];
    },
    resetForm() {
      this.form = {
        id: null,
        title: '',
        content: ''
      };
    }
  },
  mounted() {
    this.load(); // Load articles when component is mounted
  }
};
</script>

<style scoped>
/* Gaya untuk input, textarea, dan tombol */
.input-field {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #f36a6a;
  border-radius: 5px;
  box-sizing: border-box;
  font-size: 16px;
}

.btn {
  padding: 10px 20px;
  background-color: #fd6c6c;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s ease;
}

.btn:hover {
  background-color: #b30000;
}

/* Gaya untuk daftar artikel */
.article {
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #8b0000;
  border-radius: 5px;
  background-color: #ffe6e6;
}

.article h3 {
  margin-top: 0;
}

.edit-btn,
.delete-btn,
.load-btn {
  padding: 8px 12px;
  margin-top: 10px;
  background-color: #8b0000;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s ease;
}

.edit-btn:hover,
.delete-btn:hover,
.load-btn:hover {
  background-color: #b30000;
}
</style>
