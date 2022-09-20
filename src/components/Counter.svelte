<script>
    import { onMount } from "svelte"
    import moment from 'moment'
    // export let deadline
    export let end = ''
    let nw = moment()
    const dl = moment(end)
    let dr = moment.duration(nw.diff(dl))
    const dt = new Date(end)
    const now = new Date()
    let seconds = 60 - now.getSeconds()
    let minutes = 60 - now.getMinutes()
    let hours = 23 - now.getHours()
    let day = dt.getDate() - now.getDate()

    onMount(async ()=>{
        if(day === 0){
            hours = dt.getHours() - now.getHours()
            if(hours === 0){
                minutes = dt.getMinutes() - now.getMinutes()
            }
        }
        const interval = setInterval(()=>{
            timeManager()
        }, 1000)
        return ()=>{
            clearInterval(interval)
        }
    })

const timeManager = ()=>{
    nw = moment()
    dr = moment.duration(nw.diff(dl))
    // if(seconds === 0){
    //     seconds = 59
    //     minutes -= 1 
    // }
    // if(minutes === 0){
    //     minutes = 59
    //     hours -= 1 
    // }
    // if(hours === 0){
    //     hours = 23
    //     day -= 1 
    // }
    // seconds --
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
        <span>{dr.days()}</span>
        <span class="titleind">D</span>
    </div>
    <div class="divbox">
        <span>{digformat(dr.hours() * -1)}</span>
        <span class="titleind">H</span>
    </div>
    <div class="divbox">
        <span>{digformat(dr.minutes() * -1)}</span>
        <span class="titleind">M</span>
    </div>
    <div class="divbox">
        <span>{digformat(dr.seconds() * -1)}</span>
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