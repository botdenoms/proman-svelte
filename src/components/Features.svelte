<script>
    let feature = ''
    let description = ''
    let selected = 0

    const add = ()=>{
        if(selected === 0) return
        if(feature === '') return alert("feature is required")
        if(description === '') return alert("description is required")
        // add record to db
        alert("selected not equal to zero")
    }
    const reset = ()=>{
        feature = ''
        description = ''
    }
</script>

<div class="box">
    <div class="stories">
        <span>User Stories</span>
        <div class="items">
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
        <div class="more">
            <span>title</span>
            <div class="content">
                Lorem ipsum dolor, sit amet consectetur adipisicing
            </div>
        </div>
    </div>
    <div class="features">
        <span>Features in story</span>
        <div class="items">    
        </div>
    </div>
</div>

<style>
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