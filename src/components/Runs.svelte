<script>
    let custom = false
    let aval = -1
    let run = -1
    let doneIdx = -1

    $:sprints = [
        {
            name:"Sprint one",
            stories: 5,
            features: 12,
            time: 5,
            division: 'Days',
            status: 0
        },
        {
            name:"Sprint old",
            stories: 1,
            features: 2,
            time: 1,
            division: 'Days',
            status: 2
        },
        {
            name:"Sprint two",
            stories: 4,
            features: 8,
            time: 2,
            division: 'Days',
            status: 1
        }
    ]

    $:available = sprints.filter((i)=>i.status === 0)
    $:running = sprints.filter((i)=>i.status === 1)
    $:done = sprints.filter((i)=>i.status === 2)

    const customChange = ()=>{
        custom = !custom
    }

    const selectAval = (/** @type {number} */ idx)=>{
        run = -1
        doneIdx = -1
        if (aval === idx) {
            aval = -1
        }else{
            aval = idx
        }
    }

    const selectRun = (/** @type {number} */ idx)=>{
        aval = -1
        doneIdx = -1
        if (run === idx) {
            run = -1
        }else{
            run = idx
        }
    }

    const selectDone = (/** @type {number} */ idx)=>{
        run = -1
        aval = -1
        if (doneIdx === idx) {
            doneIdx = -1
        }else{
            doneIdx = idx
        }
    }

    const runSprint = ()=>{
        if(running.length > 0){
            alert("Cannot run two sprints at the same time")
            return
        }
        // logic to start a new sprint
    }
</script>

<div class="wrapper">
    <div class="sprints">
        <span>Available</span>
        <div class="items">
            {#each available as sprt, i}
                <div  class="{aval === i? 'item selected' : 'item'}" on:click={()=>selectAval(i)}>
                    {sprt.name}
                </div>
            {/each}
        </div>
        <span>Running</span>
        <div class="items">
            {#each running as sprt, i}
                <div  class="{run === i? 'item selected' : 'item'}" on:click={()=>selectRun(i)}>
                    {sprt.name}
                </div>
            {/each}
        </div>
        <span>Done</span>
        <div class="items">
            {#each done as sprt, i}
                <div  class="{doneIdx === i? 'item selected' : 'item'}" on:click={()=>selectDone(i)}>
                    {sprt.name}
                </div>
            {/each}
        </div>
    </div>
    <div class="manager">
        <div class="running">
            No running sprints
        </div>
        {#if aval !== -1}
            <div class="run">
                <div class="control">
                    {available[aval].name}
                    <button on:click={()=>runSprint()}>Run</button>
                </div>
                <div class="tile">
                    No of stories: <span>{available[aval].stories}</span>
                </div>
                <div class="tile">
                    No of features: <span>{available[aval].features}</span>
                </div>
                <div class="tile">
                    Estimated time: <span>{available[aval].time} {available[aval].division}</span>
                </div>
                <div class="custom">
                    Use custom time:
                    <input type="checkbox" on:click={customChange}>
                    {#if custom}
                        <div class="more">
                            <input type="number" placeholder=1>
                            <select name="time" value=1>
                                <option value=0>Hour(s)</option>
                                <option value=1>Day(s)</option>
                                <option value=2>Week(s)</option>
                                <option value=3>Month(s)</option>
                            </select>
                        </div>
                    {/if}
                    
                </div>
            </div>
        {:else if doneIdx !== -1}
            <div class="run">
                <div class="control">
                    {done[doneIdx].name}
                    <span class="done">Finished</span>
                </div>
                <div class="tile">
                    No of stories: <span>{done[doneIdx].stories}</span>
                </div>
                <div class="tile">
                    No of features: <span>{done[doneIdx].features}</span>
                </div>
                <div class="tile">
                    Estimated time: <span>{done[doneIdx].time} {done[doneIdx].division}</span>
                </div>
            </div> 
        {:else if run !== -1}
            <div class="run">
                <div class="control">
                    {running[run].name}
                    <span class="alert">Running</span>
                </div>
                <div class="tile">
                    No of stories: <span>{running[run].stories}</span>
                </div>
                <div class="tile">
                    No of features: <span>{running[run].features}</span>
                </div>
                <div class="tile">
                    Estimated time: <span>{running[run].time} {running[run].division}</span>
                </div>
            </div>
        {/if}
    </div>
</div>

<style>
    .done{
        color: green;
    }
    .alert{
        color: red;
    }
    input{
        margin: 0 10px;
        font-size: 17px;
        color: #1e1e1e;
        background: #e9e9e9;
        padding: 5px;
        border-radius: 5px;
        border-style: none; 
    }
    input:focus{
        outline-style: none;
        border-left: 5px solid #228bb8;
        border-radius: 0;
    }
    select{
        font-size: 17px;
        color: #1e1e1e;
        background: #e9e9e9;
        padding: 5px;
        border-radius: 5px;
        border-style: none;
    }
    select:focus{
        outline-style: none;
    }
    .custom{
        display: flex;
        justify-content: center;
        align-items: center;
        user-select: none;
        margin: 5px 0;
        font-size: 17px;
        color: #1e1e1e;
    }
    .tile{
        user-select: none;
        margin: 5px 0;
        font-size: 17px;
        color: #1e1e1e;
    }
    .tile span{
        font-weight: 800;
        font-size: 17px;
        color: #288bb2;
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
    .control{
        font-size: 20px;
        color: #1e1e1e;
        width: 100%;
        display: flex;
        justify-content: space-between;
        padding-bottom: 2px;
        border-bottom: 1px solid #1e1e1e;
    }
    .run{
        margin: 5px 10px;
        padding: 10px;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
        box-shadow: 0 3px 2px rgba(0, 0, 0, .4);
    }
    .running{
        margin: 0 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        box-shadow: 0 3px 2px rgba(0, 0, 0, .4);
    }
    .manager{
        display: grid;
        grid-template-rows: 1fr 1fr;
    }
    .selected{
        background: #fff;
    }
    .items{
        margin: 10px 0;;
        min-height: 10px;
    }
    .item{
        padding: 5px;
        margin: 5px 0;
        cursor: pointer;
        font-size: 18px;
        color: #1e1e1e;
        user-select: none;
    }
    .wrapper{
        width: 100%;
        display: grid;
        grid-template-columns: 20% 1fr;
    }

    .sprints{
        padding: 20px 0;
        display: flex;
        flex-direction: column;
        background: #c1c1c1;
    }

    .sprints span{
        margin-left: 10px;
        font-size: 15px;
        color: #288bb2;
        user-select: none;
    }
</style>