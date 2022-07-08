<script>
    import Story from "./Story.svelte"

    let user = ''
    let userstory = ''
    let criteria = ''
    let estimate = 1
    let priority = 2
    let division = 2

</script>
<div class="availables">
    <span>Available</span>
    <div class="items">
        <Story user="User A" story="As User A i want x to do y"/>
        <Story user="User B" story="As User A i want x to do y"/>
    </div>
    <div class="spacer"></div>
</div>
<div class="newstory">
    <span>Add a user story</span>
    <div class="crucial">
        <textarea bind:value={userstory} cols="30" rows="10" placeholder="User story"></textarea>
        <textarea bind:value={criteria} cols="30" rows="10" placeholder="Acceptance criteria"></textarea>
    </div>
    <div class="others">
        <div class="prior">
            <label for="priority">priority</label>
            <select name="priority" bind:value={priority} >
                <option value=1>Low</option>
                <option value=2>Mid</option>
                <option value=3>High</option>
            </select>
        </div>
        <input type="text" placeholder="User" bind:value={user}>
        <input type="number" bind:value={estimate} placeholder=1>
        <div class="prior">
            <label for="time">time division</label>
            <select name="time" bind:value={division} >
                <option value=0>Hour(s)</option>
                <option value=1>Day(s)</option>
                <option value=2>Week(s)</option>
                <option value=3>Month(s)</option>
            </select>
        </div>
    </div>
    <div class="controls">
        <button>Add</button>
        <button class="reset">Reset</button>
    </div>
</div>

<style>
    .reset{
        background: #ff0000;
    }
    button{
        background: #228bb8;
        padding: 10px;
        outline-style: none;
        color: #fff;
        width: 100px;
        border-style: none;
        border-radius: 5px; 
    }
    input{
        margin: 0 10px;
        font-size: 17px;
        color: #1e1e1e;
        background: #e9e9e9;
        padding: 10px;
        border-radius: 5px;
        border-style: none; 
    }

    input:focus{
        outline-style: none;
        border-left: 5px solid #228bb8;
        border-radius: 0;
    }
    .others{
        margin: 10px 0;
        display: flex;
    }
    .prior{
        margin-right: 10px;
        min-width: 10ch;
        display: flex;
        flex-direction: column;
        color: #1e1e1e;
        font-size: 15px;
    }
    select{
        font-size: 18px;
        color: #1e1e1e;
        margin-top: 5px;
        background: #e9e9e9;
        padding: 5px;
        border-radius: 5px;
        border-style: none;
    }
    select:focus{
        outline-style: none;
    }
    
    .crucial textarea:focus{
        outline-style: none;
        border-style: none;
        border-left: 5px solid #228bb8;
        border-radius: 0px;
    }

    .crucial textarea{
        color: #1e1e1e;
        margin: 5px 0;
        padding: 5px;
        border-style: none;
        background: #e9e9e9;
        border-radius: 5px;
        font-size: 18px;
    }
    .availables{
        padding: 10px;
        display: grid;
        grid-template-rows: auto 1fr auto;
        min-width: 20vw;
        background: #c1c1c1;
    }
    .availables span{
        font-size: 15px;
        color: #1e1e1e;
        user-select: none;
    }
    .items{
        margin-top: 10px;
    }

    .newstory{
        display: flex;
        flex-direction: column;
        padding: 20px;
    }
    .newstory span{
        font-size: 20px;
        color: #1e1e1e;
        user-select: none;
        margin-bottom: 10px;
    } 
</style>
