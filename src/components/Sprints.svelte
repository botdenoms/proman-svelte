<script>
    let sprint = ''
    let index = -1
    $: sprints = [1]
    $: stories = [1,11,2]

    const add = () =>{
        if(!sprint) return alert("sprint name is required")
        sprint = ''
        sprints = [...sprints, 5]
    }

    const select = (/** @type {number} */ idx) =>{
        index = idx
    }

    const assign = (/** @type {number} */ idx) =>{
        if (index === -1) return
        alert(idx.toString())
        let tmp = stories.filter((v,i)=>{
            return i !== idx?true:false
        })
        stories = tmp
    }

</script>
<div class="wrapper">
    <div class="forms">
        <div class="sprintform">
            <span>Create a sprint</span>
            <input bind:value={sprint} type="text" placeholder="Sprint name">
            <button on:click={add}>Create</button>
        </div>
        <div class="sprints">
            <span>Sprints</span>
            <div class="itemslist">
                {#each sprints as sprint, i}
                    <div class="{index === i? 'item active' : 'item'}" on:click={()=>select(i)}>
                        <span>Lorem ipsum</span>
                        <span>2</span>
                    </div> 
                {/each}  
            </div>
        </div>
    </div>
    <div class="stories">
        <span>User stories</span>
        <div class="items">
            {#each stories as sty, i}
            <div class="story" on:click={()=>assign(i)}>
                <div>
                    <span id='user'>User identity</span>
                    <div class="userstory">
                        Lorem ipsum dolor sit, amet consectetur adipisicing elit. 
                        Explicabo, sed asperiores!
                    </div>
                </div>
                <div>
                    <div class="prior">
                        Priority: <span>1</span>
                    </div>
                    <div class="prior">
                        Features: <span>1</span>
                    </div>
                </div>
            </div>
            {/each}
        </div>
        <!-- <div class="spacer"></div> -->
    </div>
</div>

<style>
    .story{
        margin-right: 5px;
        background: #fff;
        cursor: pointer;
        min-width: 400px;
        max-width: 450px;
        padding: 10px;
        border-radius: 5px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .story:hover{
        border-radius: 0;
        box-shadow: 1px 3px 4px rgba(0, 0, 0, .3);
    }
    .items{
        padding: 5px;
        justify-content: stretch;
        overflow-x: scroll;
        display: flex;
        align-items: stretch;
        height: 100%;
    }

    .userstory{
        margin-top: 10px;
        margin-bottom: 20px;
        color:#1e1e1e;
        font-size: 19px;
    }
    #user{
        color: #228bb8;
    }
    .prior{
        color: #228bb8;
        font-size: 17px;
    }
    .stories{
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: stretch;
        margin-top: 2px;
        margin-bottom: 2px;
        background: #c1c1c1;
        padding: 10px;
        max-height: 50vh;
        overflow: hidden;
    }
    .stories span{
        color: #1e1e1e;
        margin-bottom: 10px;
    }
    .sprints{
        overflow-y: scroll;
        padding: 10px;
        display: grid;
        grid-template-rows: auto 1fr;
        min-width: 20vw;
        background: #c1c1c1;
    }

    .sprints span{
        font-size: 15px;
        color: #1e1e1e;
        user-select: none;
    }
    .item{
        padding: 5px;
        margin: 2px 0;
        cursor: pointer;
        display: flex;
        justify-content: space-between;
    }

    .active{
        border-bottom: 1px solid #228bb8;
    }

    .active span{
        color: #228bb8;
    }
    .wrapper{
        overflow-x: hidden;
        width: 100vw;
        display: grid;
        grid-template-rows: 40% 60%;
    }

    .forms{
        display: flex;
        justify-content: space-between;
    }

    .sprintform{
        display: flex;
        flex-direction: column;
        padding: 20px;
        color: #1e1e1e;
    }

    .sprintform span{
        font-size: 20px;
        user-select: none;
    }

    input:focus{
        outline-style: none;
        border-left: 5px solid #228bb8;
        border-radius: 0;
    }

    button{
        cursor: pointer;
        background: #228bb8;
        padding: 10px;
        outline-style: none;
        color: #fff;
        width: 100px;
        border-style: none;
        border-radius: 5px; 
    }
    input{
        margin: 10px 0;
        font-size: 17px;
        color: #1e1e1e;
        background: #e9e9e9;
        padding: 10px;
        border-radius: 5px;
        border-style: none; 
    }
</style>