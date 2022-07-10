<script>
    let feature = ''
    let description = ''
    let selected = -1

    $:stories = [
        {
            user: "denoms",
            story: "Lorem ipsum dolor, sit amet consectetur adipisicing"
        },
        {
            user: "deno0ms",
            story: "Lorem ipsum dolor, sit amet consectetur adipisicing...."
        }
    ]

    $:features = [
        {
            feature: "feature verb",
            details: "Lorem ipsum dolor, sit amet consectetur adipisicing"
        }
    ]

    const selectStory = (/** @type {number} */ idx)=>{
        selected = idx
        // fetch features list with selectd story id
    }
    const add = ()=>{
        if(selected === -1) return
        if(feature === '') return alert("feature is required")
        if(description === '') return alert("description is required")
        // add record to db on the selected story
        alert("selected not equal to zero")
    }
    const reset = ()=>{
        feature = ''
        description = ''
    }
    const remove = (/** @type {number} */ idx)=>{
        alert(`remove fearure ${idx}`)
    }
</script>

<div class="box">
    <div class="stories">
        <span>User Stories</span>
        <div class="items">
            {#each stories as story, i}
                <div class="{selected === i? 'item selected' : 'item'}" on:click={()=>selectStory(i)}>
                    <span>{story.user}</span>
                </div>
            {/each}
        </div>
    </div>
    <div class="featureform">
        <span>Feature</span>
        <input type="text" placeholder="Feature" bind:value={feature}>
        <textarea bind:value={description} cols="30" rows="5" placeholder="feature description..."></textarea>
        <div class="controls">
            <button on:click={add}>Add</button>
            <button id="reset" on:click={reset}>Reset</button>
        </div>
        {#if stories.length>0 && selected !== -1}
            <div class="more">
                <span>{stories[selected].user}</span>
                <div class="content">
                    {stories[selected].story}
                </div>
            </div>
        {/if}
    </div>
    <div class="features">
        <span>Features in story</span>
        {#if selected !== -1}
            <div class="items">
                {#each features as feat,i}
                    <div class="feat">
                        <div class="top">
                            <span>{feat.feature}</span>
                            <button on:click={()=>remove(i)} class="close">X</button>
                        </div>
                        <div class="content">
                            {feat.details}
                        </div>
                    </div>
                {/each}   
            </div>
        {:else}
            <div class="plc">
                <span>Select a story to see features</span>
            </div>
        {/if}
    </div>       
</div>

<style>
    .feat{
        padding: 5px;
        margin: 2px 0;
        background: #fff;
        display: flex;
        flex-direction: column;
        height: 30px;
    }
    .feat .content{
        color: #1e1e1e;
        font-size: 18px;
        margin: 2px 0;
        visibility: hidden;
    }
    .feat .top{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .feat .close{
        width: 28px;
        height: 28px;
        background: red;
        color: #fff;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        text-transform: uppercase;
        font-weight: bold;
        visibility: hidden;
    }
    .feat:hover{
        height: auto;
    }
    .feat:hover .close{
        visibility: visible;
    }

    .feat:hover .content{
        visibility: visible;
    }
    .plc{
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .selected{
        background-color: #fff;
    }
    .item{
        padding: 5px;
        margin: 2px 0;
        cursor: pointer;
    }
    .item span{
        color: #1e1e1e;
        font-size: 18px;
        text-transform: capitalize;
    }
    .more{
        margin-top: 20px;
        display: block;
        padding: 10px 0;
    }
    .more span{
        color: #1e1e1e;
        text-transform: capitalize;
    }
    .more .content{
        margin-top: 10px;
        color: #1e1e1e;
        font-size: 18px;
    }
    .features span{
        font-size: 15px;
        color: #1e1e1e;
        user-select: none;
    }
    .features{
        overflow-y: scroll;
        padding: 10px;
        display: grid;
        grid-template-rows: auto 1fr;
        min-width: 20vw;
        /* max-height: 85vh; */
        background: #c1c1c1; 
    }
    .controls{
        margin: 10px 0;
    }
    .featureform{
        display: flex;
        flex-direction: column;
        padding: 20px;
    }

    .featureform span{
        font-size: 20px;
        color: #1e1e1e;
        user-select: none;
    }
    .items{
        margin-top: 10px;
    }
    .stories span{
        font-size: 15px;
        color: #1e1e1e;
        user-select: none;
    }
    .stories{
        overflow-y: scroll;
        padding: 10px;
        display: grid;
        grid-template-rows: auto 1fr;
        min-width: 20vw;
        /* max-height: 85vh; */
        background: #c1c1c1; 
    }
    .box{
        width: 100%;
        display: grid;
        grid-template-columns: auto 1fr auto;
    }

    #reset{
        background: red;
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

    textarea:focus{
        outline-style: none;
        border-style: none;
        border-left: 5px solid #228bb8;
        border-radius: 0px;
    }

    textarea{
        color: #1e1e1e;
        margin: 10px 0;
        padding: 5px;
        border-style: none;
        background: #e9e9e9;
        border-radius: 5px;
        font-size: 18px;
    }
</style>