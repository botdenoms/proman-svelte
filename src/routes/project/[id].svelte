<script context="module">
    export async function load({params, fetch}){
        const id = params.id
        const url = `http://localhost:5000/projects/${id}`
        const res = await fetch(url)
        const project = await res.json()
        return {
            props: {project}
        }
        // if(res.ok){
        //     const project = await res.json()
        //     return {
        //         props: {project}
        //     }
        // }
    }
</script>
<script>
    // import {onMount} from 'svelte'

    // import {page} from '$app/stores'
    import UserStories from '../../../src/components/UserStories.svelte'
    import Features from '../../../src/components/Features.svelte'
    import Sprints from '../../../src/components/Sprints.svelte'
    import Runs from '../../../src/components/Runs.svelte'
    // const id = $page.params.id
    // onmount use id to fetch project data
    // onMount( async ()=>{
    //     // 127.0.0.1:port
    //     let url = 'http://localhost:5000/projects/' + id
    //     let resp = await fetch(url)
    //     // then(response => response.json()).then(data=>console.log(data)).catch(error=>console.log(error))
    //     let data = await resp.json()
    //     // console.log(data)
    //     project = data
    // })

    export /**
* @type {{ name: any; } | undefined}
*/
     let project
    let idx = 0
    const tabChange = (/** @type {any} */ index)=>{
        idx = index
    }

    const addStory = async(data)=>{
        project = {...project, stories: [...data]}
        console.log(project);
        fetch(`http://localhost:5000/projects/${project.id}`, {
            
                method:'PUT',
                headers: {
                    'Content-type' :'application/json'
                },
                body: JSON.stringify({...project})
            }).then(resp=>resp.json())
            .then(newdt => (console.log(newdt)))
    }

    const addFeature = async(data)=>{
        project = {...project, features: [...data]}
        console.log(project);
        fetch(`http://localhost:5000/projects/${project.id}`, {
            
                method:'PUT',
                headers: {
                    'Content-type' :'application/json'
                },
                body: JSON.stringify({...project})
            }).then(resp=>resp.json())
            .then(newdt => (console.log(newdt)))
    }

    const addSprint = async(data)=>{
        project = {...project, sprints: [...data]}
        console.log(project);
        fetch(`http://localhost:5000/projects/${project.id}`, {
            
                method:'PUT',
                headers: {
                    'Content-type' :'application/json'
                },
                body: JSON.stringify({...project})
            }).then(resp=>resp.json())
            .then(newdt => (console.log(newdt)))
    }

</script>
<div class="container">
    <div class="topbar">
        <div class="logobox">
            <div class="logo"></div>
            <span>Proman</span>
        </div>
        {#if project === undefined}
            <span></span>
        {:else}
            <span class="name">{project.name} </span>
        {/if}
        <!-- {project === undefined?<span></span>:<span class="name"></span>} -->
        <div></div>
    </div>
    <div class="main">
        <div class="tab">
            <div class="{idx === 0? 'option active' : 'option'}" on:click={()=> tabChange(0)}>
                <span>User Stories</span>
            </div>
            <div class="{idx === 1? 'option active' : 'option'}" on:click={()=> tabChange(1)}>
                <span>Features</span>
            </div>
            <div class="{idx === 2? 'option active' : 'option'}" on:click={()=> tabChange(2)}>
                <span>Sprints</span>
            </div>
            <div class="{idx === 3? 'option active' : 'option'}" on:click={()=> tabChange(3)}>
                <span>Runs</span>
            </div>
        </div>
        <div class="content">
            {#if idx === 0}
                <UserStories stories={project.stories} {addStory}/>
            {:else if idx === 1}
                <Features stories={project.stories} features={project.features} {addFeature}/>
            {:else if idx === 2}
                <Sprints stories={project.stories} sprints={project.sprints} features={project.features} {addSprint}/>
            {:else}
                <Runs/>
            {/if}
        </div>
    </div>
</div>

<style>
    :global(body) {
        overflow: hidden;
        margin: 0;
        padding: 0;
    }
    .container{
        display: grid;
        height: 100vh;
        grid-template-rows: auto 1fr;
    }

    .topbar{
        display: flex;
        justify-content: space-between;
        align-items: center;
        background: #c1c1c1;
    }

    .name{
        color: #1e1e1e;
        font-size: 24px;
        user-select: none;
        cursor: pointer;
    }

    .logobox{
        display: flex;
        align-items: center;
        padding: 10px;
    }

    .logobox span{
        color: #1e1e1e;
        font-size: x-large;
        user-select: none;
        cursor: pointer;
        margin-left: 10px;
    }
    .logo{
        width: 20px;
        height: 20px;
        background: #1e1e1e;
        border-radius: 5px;
    }

    .main{
        display: grid;
        grid-template-rows: auto 1fr;
    }

    .option{
        padding: 5px;
    }

    .option span{
        color: #1e1e1e;
        font-size: 18px;
        user-select: none;
        cursor: pointer;
    }

    .option.active{
        border-bottom: 2px solid #288bb8;
    }
    .option.active span{
	color: #288bb8;
    }

    .tab{
        display: flex;
    }

    .content{
        display: flex;
        justify-content: flex-start;
        align-items: stretch;
    }
</style>