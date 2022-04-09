<template>
    <h1>Credentials</h1>
    <div v-if="creds.length"> 
            <div v-for="cred in creds" :key="cred.id" class="cred">  
                <router-link :to="{name: 'JobDetails', params: { id: cred.id }}"> 
                    <h2> {{ cred.uname }} : {{ cred.pwd }}</h2>
                </router-link>
            </div>      
        </div>
     <div v-else>
        <p>Loading Credentials...</p>
      </div>
    
</template>

<script>
export default {
    data() {
        return {
            creds: []
        }
    },
    mounted() {
        fetch('http://localhost:3000/creds')
            .then((res) => res.json())
            .then(data => this.creds = data)
            .catch(err => console.log(err.message))
    } 
}

</script>

<style>
.creds h2{
    background: #f4f4f4;
    padding: 20px;
    border-radius: 10px;
    margin: 10px auto;
    max-width: 600px;
    cursor: pointer;
    color: #444;
}

.creds h2:hover {
    background: #ddd;
}

.creds a{
    text-decoration: none;
}
</style>