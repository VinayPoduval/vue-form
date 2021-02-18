<template>
    <div class="container bg-dark p-3">
        <h1 class="text-white text-center">Fill Form</h1>
    </div>
    <div class="container bg-light p-3">
        <div v-if="loading">
            <h2>Submitting Form</h2>
            <div class="text-center p-3">
                <div class="spinner-border"></div>
            </div>
        </div>
        <form v-if="!loading" id="form" @submit="handleSubmit">
            <div class="form-group">
                <label for="name">Name:</label>
                <input type="text" class="form-control" id="name" placeholder="Enter name.." required v-model="name">
            </div>
            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" class="form-control" id="email" placeholder="Enter email.." required v-model="email">
            </div>
            <div class="form-group">
                <label for="contact">Contact No.:</label>
                <input type="tel" class="form-control" id="phone" placeholder="Enter contact no. .." required v-model="phone">
                <!--<div class="error" v-if="phoneErr">
                    <p>{{phoneErr}}</p>
                </div>-->
            </div>
            <div class="form-group">
                <label for="role">Applying for:</label>
                <select class="form-control" v-model="role">
                    <option value="default">Choose role</option>
                    <option value="Web Developer">Web Developer</option>
                    <option value="Software Tester">Software Tester</option>
                    <option value="Web Designer">Web Designer</option>
                </select>
            </div>
            <div class="text-center p-3">
                <button type="submit" class="btn btn-primary btn-lg">Submit</button>
            </div>
        </form>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            name: '',
            email: '',
            phone: '',
            role: 'default',
            loading: false
        }
    },
    methods: {
        handleSubmit(e) {
            e.preventDefault()
            this.loading = true
            const name = this.name
            const email = this.email
            const phone = this.phone
            const role = this.role
            const newData = {
                name,
                email,
                phone,
                role
            }
            this.sendData(newData)
        },
        async sendData(newData) {
            try {
                const res = await axios.post('https://wanom.api.stdlib.com/vue-form@dev/', {newData})
                if(res.status === 200) {
                    this.name = this.email = this.phone = '' 
                    this.role = 'default'
                    this.loading = false
                    alert('Form submitted successfully')
                }
                else {
                    alert(`There was an error ${res.status}`)
                }
            }
            catch(e) {
                console.error(e)
            }
        }
    }
}
</script>

<style>
    .error {
        color: crimson;
    }
</style>