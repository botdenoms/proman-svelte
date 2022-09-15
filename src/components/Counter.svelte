<script>
import { onMount } from "svelte";
    // export let deadline
    const dt = new Date('2022-09-17T03:24:00')
    const now = new Date()
    let seconds = 60 - now.getSeconds()
    let minutes = 60 - now.getMinutes()
    let hours = 23 - now.getHours()
    let day = dt.getDay() - now.getDay()

onMount(async ()=>{
    if(day === 0){

    }
    const interval = setInterval(()=>{
        timeManager()
    }, 1000)
    return ()=>{
        clearInterval(interval)
    }
})

const timeManager = ()=>{
    if(seconds === 0){
        seconds = 59
        minutes -= 1 
    }
    if(minutes === 0){
        minutes = 59
        hours -= 1 
    }
    if(hours === 0){
        hours = 23
        day -= 1 
    }
    seconds --
}

const digformat = (value)=>{
    if(value < 10){
        return `0${value}`
    }
    return value
}

</script>

<div class="container">
    <div class="divbox">
        <span>{digformat(day)}</span>
        <span class="titleind">D</span>
    </div>
    <div class="divbox">
        <span>{digformat(hours)}</span>
        <span class="titleind">H</span>
    </div>
    <div class="divbox">
        <span>{digformat(minutes)}</span>
        <span class="titleind">M</span>
    </div>
    <div class="divbox">
        <span>{digformat(seconds)}</span>
        <span class="titleind">S</span>
    </div>
</div>

<style>
    .container{
        display: flex;
    }

    .divbox{
        display: flex;
    }
    .titleind{
        color: red;
        margin: 0 5px;
    }
</style>