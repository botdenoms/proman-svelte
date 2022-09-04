<script>
    import {goto} from '$app/navigation'

    $:projects = [
        {
            id: 1,
            name: "Test Project 1"
        },
        {
            id: 2,
            name: "Project 101"
        },
        {
            id: 3,
            name: "Kill  the goat"
        }
    ]

    let name = ''
    let description = ''

    const createPoject = (/** @type {string} */ name) =>{
        if(!name){
            alert('A project name is required')
        } else if (!description) {
            alert('A project description is required')
        } else {
            // create project in db
            const pid = projects.length + 1
            projects = [...projects, {id:pid, name: name}]
            description = ''
            name = ''
            goto(`/project/${projects[projects.length - 1].id}`,{replaceState: false})
        }
    }
</script>

<svelte:head>
	<title>Proman</title>
</svelte:head>

<div class='main'>
    <div class='history'>
        <div class="logobox">
            <div class="logo"></div>
            <span>Proman</span>
        </div>
        <div class="title">
            <span>recents</span>
        </div>
        <div class="recents">
            {#each projects as project}
                <div class='recent'>
                    <a href='/project/{project.id}'>
                        <span>{project.name}</span>
                    </a>
                </div>
            {/each}
        </div>
    </div>
    <div class='new'>
        <span>Add a new project</span>
        <input type="text" name="name" placeholder="Project" class="name" bind:value={name}>
        <textarea 
            placeholder="description of the project..."
            class="descript" 
            bind:value={description}
            rows="4"/>
        <button class="addbtn" on:click={()=>createPoject(name)}>Create</button>
    </div>
    <div></div>
</div>

<style>
    :global(body) {
        overflow: hidden;
        margin: 0;
        padding: 0;
    }
    .main{
        height: 100vh;
        display: grid;
        grid-template-columns: 20% 1fr 1fr;
    }
    .history{
        padding: 20px;
        background: #c1c1c1;
    }

    .title{
        margin-top: 40px;
        margin-bottom: 5px;
        color: #1e1e1e;
        user-select: none;
        font-size: small;
    }

    .logobox{
        display: flex;
        align-items: center;
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

    .recents{
        display: flex;
        flex-direction: column;
    }

    .recent{
        cursor: pointer;
        margin: 2px 0;
    }
    
    .recent a{
        text-decoration: none;
        color: #1e1e1e;
        font-size: 20px;
        transition: all 200ms;
    }

    .recent:hover a{
        color: #fff;
        transition: all 500ms;
        font-size: 24px;
    }
    .new{
        margin: 50px 20px;
        display: flex;
        flex-direction: column;
    }
    .new span{
        color: #1e1e1e;
        font-size: 22px;
        user-select: none;
        margin-bottom: 5px;
    }

    .name{
        color: #1e1e1e;
        margin: 5px 0;
        padding: 5px;
        border-style: none;
        background: #e9e9e9;
        border-radius: 5px;
        font-size: 18px;
    }
    .name:focus{
        outline-style: none;
        border-style: none;
        border-left: 5px solid #228bb8;
        border-radius: 0px;
    }
    .descript:focus{
        transition: all 200ms;
        outline-style: none;
        border-style: none;
        border-left: 5px solid #228bb8;
        border-radius: 0px;
    }
    .descript{
        transition: all 500ms;
        color: #1e1e1e;
        margin: 5px 0;
        padding: 5px;
        border-style: none;
        background: #e9e9e9;
        border-radius: 5px;
        font-size: 17px;
        word-break: break-all;
    }

    .addbtn{
        background: #228bb8;
        padding: 10px;
        outline-style: none;
        color: #fff;
        width: 100px;
        border-style: none;
        border-radius: 5px;
        cursor: pointer;
    }

   
</style>