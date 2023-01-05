<template>
    <div>
        <h3>Edit Project</h3>
        <form @submit.prevent="handleSubmit">
            <label>Title: </label>
            <input type="text" v-model="title" required>
            <label>Details: </label>
            <textarea v-model="details" required></textarea>
            <button>Update Project</button>
        </form>
    </div>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            title: '',
            details: '',
            uri: 'http://localhost:3000/projects/' + this.id
        }
    },
    mounted() {
        fetch(this.uri)
            .then(res => res.json())
            .then(data => {
                this.title = data.title,
                    this.details = data.details
            });
    },
    methods: {
        handleSubmit() {
            fetch(this.uri, {
                method: 'PATCH',
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ title: this.title, details: this.details })
            })
                .then(() => this.$router.push("/"))
                .catch((err) => console.log(err))
        }
    },
}
</script>

<style>
form {
    background: #fff;
    padding: 20px;
    border-radius: 10px;
}

label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
}

input {
    padding: 10px;
    border: 0;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    width: 100%;
    box-sizing: border-box;
}

textarea {
    padding: 10px;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    border: 0;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
}

form button {
    display: block;
    margin: 20px auto 0;
    background: #2E8B57;
    padding: 10px;
    border: 0;
    font-size: 15px;
    border-radius: 7px;
    color: #fff;
}
</style>