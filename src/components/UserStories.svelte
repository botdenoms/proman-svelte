<script>
    import Story from "./Story.svelte"

    let user = ''
    let userstory = ''
    let criteria = ''
    let estimate = 1

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
        <input type="text" placeholder="User" bind:value={user}>
        <input type="number" bind:value={estimate}>
    </div>
    <div class="controls">
        <button>Add</button>
        <button>Reset</button>
    </div>
</div>

<style>
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
