<template>
    <h1>Jobs</h1>
    <div v-if="jobs.length"> 
        <div v-for="job in jobs" :key="job.id" class="job">  
            <router-link :to="{name: 'JobDetails', params: { id: job.id }}"> 
                <h2> Role: {{ job.title }} : {{ job.pack }} Lpa</h2>
            </router-link>
        </div>      
    </div>
    <div v-else>
        <p>Loading Jobs...</p>
    </div>
    
</template>

<script>
export default {
    data() {
        return {
            jobs: [
                // {title: 'UX Designer', id: 1, details: 'Need ux deigner', pack: 4.5},
                // {title: 'UI Designer', id: 2, details: 'Need ui deigner', pack: 5.5},
                // {title: 'UI/UX Designer', id: 3, details: 'Need ui/ux deigner', pack: 7.5},
            ]
        }
    },
    mounted() {
        fetch('http://localhost:3000/jobs')
            .then((res) => res.json())
            .then(data => this.jobs = data)
            .catch(err => console.log(err.message))
    } 
}

</script>

<style>
.job h2{
    background: #f4f4f4;
    padding: 20px;
    border-radius: 10px;
    margin: 10px auto;
    max-width: 600px;
    cursor: pointer;
    color: #444;
}

.job h2:hover {
    background: #ddd;
}

.job a{
    text-decoration: none;
}
</style>