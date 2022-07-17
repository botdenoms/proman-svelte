<script>
</script>

<div class="wrapper">
    <div class="sprints">
        <span>Available</span>
        <div class="items">
            <div class="item selected">
                sprint 1
            </div>
            <div class="item">
                sprint 2
            </div>
        </div>
        <span>Running</span>
        <div class="items"></div>
        <span>Done</span>
        <div class="items"></div>
    </div>
    <div class="manager">
        <div class="running">
            No running sprints
        </div>
        <div class="run">
            <div class="control">
                Sprint Name
                <button>Run</button>
            </div>
            <div class="tile">
                No of stories: <span>1</span>
            </div>
            <div class="tile">
                No of features: <span>1</span>
            </div>
            <div class="tile">
                Estimated time: <span>1 days</span>
            </div>
            <div class="custom">
                Use custom time:
                <input type="checkbox">
                <div class="more">
                    <input type="number" placeholder=1>
                    <select name="time" value=1>
                        <option value=0>Hour(s)</option>
                        <option value=1>Day(s)</option>
                        <option value=2>Week(s)</option>
                        <option value=3>Month(s)</option>
                    </select>
                </div>
            </div>
        </div>
    </div>
</div>

<style>
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