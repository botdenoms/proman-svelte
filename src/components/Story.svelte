<script>
    export let user = ''
    export let story = ''
</script>

<div class="item">
    <span>{user}</span>
    <div class="content">
        {story}
    </div>
</div>

<style>
    .item{
        margin-bottom: 5px;
    }

    .item span{
        color: #1e1e1e;
    }

    .content{
        color: #288bb2;
        border-bottom: 1px solid #474747;
    }
</style>