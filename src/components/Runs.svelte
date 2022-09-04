<script>
    let custom = false
    let aval = -1
    let run = -1
    let doneIdx = -1
    let viewid = -1

    $:sprints = [
        {
            name:"Sprint one",
            stories: [5],
            features: [12],
            time: 5,
            division: 'Days',
            status: 0
        },
        {
            name:"Sprint old",
            stories: [1],
            features: [2],
            time: 1,
            division: 'Days',
            status: 2
        },
        {
            name:"Sprint two",
            stories: [4, 5, 6],
            features: [8],
            time: 2,
            division: 'Days',
            status: 1
        }
    ]

    $:available = sprints.filter((i)=>i.status === 0)
    $:running = sprints.filter((i)=>i.status === 1)
    $:done = sprints.filter((i)=>i.status === 2)

    const more = (/** @type {number} */ idx)=>{
        viewid = idx
    }

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
        <div>
            {#if running.length === 0}
               <div class="running">
                    No running sprints
               </div> 
            {:else}
                <div class="section">
                    <div class="bar">
                        <div>
                            <span>{running[0].name}</span>
                        </div>
                        <div class="countdown">
                            <div class="dtbox"><span>1</span> D</div>
                            <div class="dtbox"><span>1</span> H</div>
                            <div class="dtbox"><span>1</span> M</div>
                            <div class="dtbox"><span>1</span> S</div>
                        </div>
                    </div>
                    <div class="checklist">
                        <div class="tabs">
                            <div class="feats">
                                Stories: <span>1/5</span>
                            </div>
                            <div class="feats">
                                Features: <span>3/18</span>
                            </div>
                        </div>
                        <div class="list">
                            {#each running[0].stories as stry, i}
                                <div class="storyitem">
                                    <div class="header">
                                        <div>
                                            <span>0%</span>
                                            <span>{stry}</span>
                                        </div>
                                        <span class="dropdwn" on:click={()=>more(i)}>></span>   
                                    </div>
                                    <div class="{viewid === i? 'features' : 'featuresoff'}">
                                        <div class="feature">
                                            <input type="checkbox">
                                            <span>features name</span>
                                        </div>
                                        <div class="feature">
                                            <input type="checkbox">
                                            <span>features name</span>
                                        </div>
                                        <div class="feature">
                                            <input type="checkbox">
                                            <span>features name</span>
                                        </div>
                                    </div>
                                </div>
                            {/each}
                        </div>
                    </div>
                </div>
            {/if}
        </div>
        {#if aval !== -1}
            <div class="run">
                <div class="control">
                    {available[aval].name}
                    <button on:click={()=>runSprint()}>Run</button>
                </div>
                <div class="tile">
                    No of stories: <span>{available[aval].stories.length}</span>
                </div>
                <div class="tile">
                    No of features: <span>{available[aval].features.length}</span>
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
                    No of stories: <span>{done[doneIdx].stories.length}</span>
                </div>
                <div class="tile">
                    No of features: <span>{done[doneIdx].features.length}</span>
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
                    No of stories: <span>{running[run].stories.length}</span>
                </div>
                <div class="tile">
                    No of features: <span>{running[run].features.length}</span>
                </div>
                <div class="tile">
                    Estimated time: <span>{running[run].time} {running[run].division}</span>
                </div>
            </div>
        {/if}
    </div>
</div>

<style>
    .featuresoff{
        display: none;
    }
    .features{
        display: flex;
    }
    .feature{
        display: flex;
        align-items: center;
    }
    .dropdwn{
        font-size: 40px;
        font-weight: bold;
        color: #1e1e1e;
        padding: 5px;
    }
    .checklist{
        margin-top: 5px;
    }
    .header{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .storyitem{
        padding: 8px;
        display: flex;
        flex-direction: column;
        cursor: pointer;
    }
    .section span{
        color: #1e1e1e;
        font-size: 18px;
    }
    .dtbox span{
        color: red;
    }
    .tabs{
        display: flex;
    }
    .countdown{
        display: flex;
    }
    .feats{
        display: flex;
        margin: 0 5px;
        cursor: pointer;
    }
    .feats span{
        color: green;
    }
    .bar{
        padding-bottom: 5px;
        display: flex;
        width: 100%;
        justify-content: space-between;
        border-bottom: #1e1e1e 1px solid;
    }
    
    .section{
        height: 100%;
        padding: 5px;
        margin: 0 10px;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        box-shadow: 0 3px 2px rgba(0, 0, 0, .4);
    }
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