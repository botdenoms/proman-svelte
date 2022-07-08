<script>
    import {page} from '$app/stores'
    import UserStories from '../../../src/components/UserStories.svelte'
    import Features from '../../../src/components/Features.svelte'
    import Sprints from '../../../src/components/Sprints.svelte'
    import Runs from '../../../src/components/Runs.svelte'
    const id = $page.params.id
    //onmount use id to fetch project data
    let idx = 0
    const tabChange = (/** @type {any} */ index)=>{
        idx = index
    }
</script>
<div class="container">
    <div class="topbar">
        <div class="logobox">
            <div class="logo"></div>
            <span>Proman</span>
        </div>
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
                <UserStories/>
            {:else if idx === 1}
                <Features/>
            {:else if idx === 2}
                <Sprints/>
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

    .logobox{
        display: flex;
        align-items: center;
        padding: 10px;
        background: #c1c1c1;
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
        justify-content: center;
        align-items: center;
    }
</style>