<template>
<h1> Job Details Page </h1>
    <div v-if="job">
        <h2> {{ job.title }} </h2>
        <!-- <p>The Job Id is : {{ $route.params.id }}</p> -->
        <p>The Job Id is : {{ id }}</p>
        <p> {{ job.details }} </p>
    </div>
    <div v-else>
        <p> Loading Job Details...</p>
    </div>
<hr>
    <h1>Credentials</h1>
    <!-- <input type="text" v-model="cred" /> -->
    <!-- <p> {{ this.creds[1] }} </p> -->
        <div v-for="cred in creds" :key="cred.id" class="cred">
            <div v-if="id">   
                <router-link :to="{name: 'JobDetails', params: { id: cred.id }}">
                    <h2> {{ id }}: {{cred.id}} : {{ cred.uname }} : {{ cred.pwd }}</h2>
                </router-link>
            </div>
        </div>   
    

</template>

<script>
export default{
    props: ['id'],
    data() {
        return {
            job: null,
            // id: this.$route.params.id
            creds: []
        }
    },
    mounted() {
        fetch('http://localhost:3000/jobs/' + this.id)
            .then((res) => res.json())
            .then(data => this.job = data)
            .catch(err => console.log(err.message)),

        fetch('http://localhost:3000/creds/')
            .then((res) => res.json())
            .then(data => this.creds = data)
            .catch(err => console.log(err.message))

    }
    // mounted() {
        // fetch('http://localhost:3000/creds/')
        //     .then((res) => res.json())
        //     .then(data => this.cred = data)
        //     .catch(err => console.log(err.message))
    // }

}

</script>


<style>
.cred h2{
    background: #f4f4f4;
    padding: 20px;
    border-radius: 10px;
    margin: 10px auto;
    max-width: 600px;
    cursor: pointer;
    color: #444;
}

.cred h2:hover {
    background: #ddd;
}

.cred a{
    text-decoration: none;
}

</style>