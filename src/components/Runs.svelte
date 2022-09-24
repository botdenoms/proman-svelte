<script>
    import Counter from './Counter.svelte'
    let custom = false
    let aval = -1
    let run = -1
    let doneIdx = -1
    let viewid = -1
    let cestimate = 1
    let cdiv = 2
    
    export let addSprint
    export let stories = []
    export let features = []
    export let sprints = [
        // {
        //     name:"Sprint one",
        //     stories: [5],
        //     features: [12],
        //     time: 5,
        //     division: 'Days',
        //     status: 0
        // },
        // {
        //     name:"Sprint old",
        //     stories: [1],
        //     features: [2],
        //     time: 1,
        //     division: 'Days',
        //     status: 2
        // },
        // {
        //     name:"Sprint two",
        //     stories: [4, 5, 6],
        //     features: [8],
        //     time: 2,
        //     division: 'Days',
        //     status: 1
        // }
    ]

    $:available = sprints.filter((i)=>i.status === 0)
    $:running = sprints.filter((i)=>i.status === 1)
    $:done = sprints.filter((i)=>i.status === 2)

    const more = (/** @type {number} */ idx)=>{
        if (viewid === idx){
            viewid = -1
            return
        }
        viewid = idx
    }

    const featuresNo = (strlist)=>{
        let count = 0
        strlist.forEach(strid => {
            features.forEach(element => {
                if(element.storyId === strid){
                    count ++
                }
            })  
        })
        return count
    }

    const timeFromStroies = (strlist)=>{
        let mcount = 0
        let wcount = 0
        let dcount = 0
        let hcount = 0 
        strlist.forEach(strid => {
            stories.forEach(element => {
                if(element.id === strid){
                    if(element.division === 0){
                        hcount += element.estimate
                    }
                    if(element.division === 1){
                        dcount += element.estimate
                    }
                    if(element.division === 2){
                        wcount += element.estimate
                    }
                    if(element.division === 3){
                        mcount += element.estimate
                    }
                }
            })
        })
        return `${mcount}M ${wcount}W ${dcount}D ${hcount}H`
    }

    const storyName = (stryId)=>{
        let trg = stories.filter((s)=>s.id === stryId)
        // console.log(trg)
        return trg[0].user
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
        // check if stories is > features, need future improvements
        if(available[aval].stories.length > featuresNo(available[aval].stories)){
            alert("User stories needs to have at least one feature ")
            return
        }
        let trans = available[aval]
        let temp = sprints.filter((i)=>i.id !== available[aval].id)
        trans.status = 1
        let start = new Date() 
        // '2022-09-17T03:24:00
        if(custom){
            if(cdiv === 0){
                let yr = start.getFullYear()
                let mnt = (start.getMonth() + 1).toString().padStart(2, '0')
                let dt = start.getDate().toString().padStart(2, '0')
                let hr = (start.getHours() + cestimate).toString().padStart(2, '0')
                let mn = start.getMinutes().toString().padStart(2, '0')
                let sc = start.getSeconds().toString().padStart(2, '0')
                trans.end = `${yr}-${mnt}-${dt}T${hr}:${mn}:${sc}`
            } else if(cdiv === 1){
                let yr = start.getFullYear()
                let mnt = (start.getMonth() + 1).toString().padStart(2, '0')
                let hr = start.getHours().toString().padStart(2, '0')
                let dt = (start.getDate() + cestimate).toString().padStart(2, '0')
                let mn = start.getMinutes().toString().padStart(2, '0')
                let sc = start.getSeconds().toString().padStart(2, '0')
                trans.end = `${yr}-${mnt}-${dt}T${hr}:${mn}:${sc}`
            }else if(cdiv === 2){
                let yr = start.getFullYear()
                let mnt = (start.getMonth() + 1).toString().padStart(2, '0')
                let hr = start.getHours().toString().padStart(2, '0')
                let dt = (start.getDate() + (cestimate * 7)).toString().padStart(2, '0')
                let mn = start.getMinutes().toString().padStart(2, '0')
                let sc = start.getSeconds().toString().padStart(2, '0')
                trans.end = `${yr}-${mnt}-${dt}T${hr}:${mn}:${sc}`
            }else{
                let yr = start.getFullYear()
                let mnt = (start.getMonth() + 1 + cestimate).toString().padStart(2, '0')
                let hr = start.getHours().toString().padStart(2, '0')
                let dt = start.getDate().toString().padStart(2, '0')
                let mn = start.getMinutes().toString().padStart(2, '0')
                let sc = start.getSeconds().toString().padStart(2, '0')
                trans.end = `${yr}-${mnt}-${dt}T${hr}:${mn}:${sc}`
            }
        }else{
            let mcount = 0
            let wcount = 0
            let dcount = 0
            let hcount = 0 
            available[aval].stories.forEach(strid => {
                stories.forEach(element => {
                    if(element.id === strid){
                        if(element.division === 0){
                            hcount += element.estimate
                        }
                        if(element.division === 1){
                            dcount += element.estimate
                        }
                        if(element.division === 2){
                            wcount += element.estimate
                        }
                        if(element.division === 3){
                            mcount += element.estimate
                        }
                    }
                })
            })
            if(hcount > 0 || dcount > 0 || wcount > 0 || mcount){
                let yr = start.getFullYear()
                let mnt = (start.getMonth() + 1 + mcount).toString().padStart(2, '0')
                let dt
                if(wcount > 0 && dcount > 0){
                    dt = (start.getDate() + (wcount * 7) + dcount).toString().padStart(2, '0')
                }else{
                    if(wcount > 0){
                        dt = (start.getDate() + (wcount * 7)).toString().padStart(2, '0')
                    }else{
                        dt = (start.getDate() + dcount).toString().padStart(2, '0')
                    }
                }
                let hr = (start.getHours() + hcount).toString().padStart(2, '0')
                let mn = start.getMinutes().toString().padStart(2, '0')
                let sc = start.getSeconds().toString().padStart(2, '0')
                trans.end = `${yr}-${mnt}-${dt}T${hr}:${mn}:${sc}`
            }else{
                return alert("Cannot start the sprint")
            }
            // trans.end = """
        }
	    aval = -1
	    run = -1
    	doneIdx = -1
        sprints = [...temp, trans]
        addSprint(sprints)
        available = sprints.filter((i)=>i.status === 0)
        running = sprints.filter((i)=>i.status === 1)
        done = sprints.filter((i)=>i.status === 2)
    }

    const markFeat = (ftid, strid)=>{
        alert(`${ftid}, ${strid}`)
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
                        <Counter end={running[0].end}/>
                    </div>
                    <div class="checklist">
                        <div class="tabs">
                            <div class="feats">
                                Stories: <span>1/{running[0].stories.length}</span>
                            </div>
                            <div class="feats">
                                Features: <span>3/{featuresNo(running[0].stories)}</span>
                            </div>
                        </div>
                        <div class="list">
                            {#each running[0].stories as stry, i}
                                <div class="storyitem">
                                    <div class="header">
                                        <div>
                                            <span>0%</span>
                                            <span>{storyName(stry)}</span>
                                        </div>
                                        <span class="dropdwn" on:click={()=>more(i)}>></span>   
                                    </div>
                                    <div class="{viewid === i? 'features' : 'featuresoff'}">
                                        {#each features as ft , ind}
                                            {#if ft.storyId === stry}
                                                <div class="feature">
                                                    <input type="checkbox" on:change={markFeat(ft.id, stry)}>
                                                    <span>{ft.feature}</span>
                                                </div>
                                            {/if}
                                        {/each}
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
                    No of features: <span>{featuresNo(available[aval].stories)}</span>
                </div>
                <div class="tile">
                    Estimated time: <span>{timeFromStroies(available[aval].stories)}</span>
                </div>
                <div class="custom">
                    Use custom time:
                    <input type="checkbox" bind:checked={custom}>
                    {#if custom}
                        <div class="more">
                            <input type="number" placeholder=1 bind:value={cestimate}>
                            <select name="time" bind:value={cdiv}>
                                <option value={0}>Hour(s)</option>
                                <option value={1}>Day(s)</option>
                                <option value={2}>Week(s)</option>
                                <option value={3}>Month(s)</option>
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
                    No of features: <span>{featuresNo(done[doneIdx].stories)}</span>
                </div>
                <div class="tile">
                    Estimated time: <span>{timeFromStroies(done[doneIdx].stories)}</span>
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
                    No of features: <span>{featuresNo(running[run].stories)}</span>
                </div>
                <div class="tile">
                    Estimated time: <span>{timeFromStroies(running[run].stories)}</span>
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
    .tabs{
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
        height: 100%;
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