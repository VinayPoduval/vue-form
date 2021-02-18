<template>
    <div class="container bg-dark p-3">
        <h1 class="text-white text-center">Fill Form</h1>
    </div>
    <div class="container bg-light p-3">
        <form id="form" @submit="handleSubmit">
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
                <div class="error" v-if="phoneErr">
                    <p>{{phoneErr}}</p>
                </div>
            </div>
            <div class="form-group">
                <label for="role">Applying for:</label>
                <select class="form-control" v-model="role">
                    <option value="default">Choose role</option>
                    <option value="developer">Web Developer</option>
                    <option value="tester">Software Tester</option>
                    <option value="designer">Web Designer</option>
                </select>
            </div>
            <div class="text-center p-3">
                <button type="submit" class="btn btn-primary btn-lg">Submit</button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: '',
            email: '',
            phone: '',
            phoneErr: '',
            role: 'default'
        }
    },
    methods: {
        handleSubmit(e) {
            e.preventDefault()

            this.phone.length === 10 ? 
                '' : this.phoneErr = '*Contact no. should be 10 digits'
        }
    }
}
</script>

<style>
    .error {
        color: crimson;
    }
</style>