<template>
    <div id="chess">
        <section class="chess-box">
            <div v-for="item of 9" class="chess-item" @click="onClick(item-1)">{{map[item-1]}}</div>
        </section>
        <div>{{res}}</div>
    </div>
</template>

<script>
export default {
    data:()=>({
        map:[null,null,null,null,null,null,null,null,null],
        map2:[
            [null,null,null],
            [null,null,null],
            [null,null,null]
        ],
        num:0,
        res:'胜负未分',
        isEnd:false
    }),
    methods:{
        // 下棋
        onClick(i){
            //比赛已结束
            if(this.isEnd){return}

            this.num++
            //奇数偶数
            let value = this.num%2 == 0 ? 'x' : 'o'
            
            //视图
            this.$set(this.map,i,value)
            //用来判断胜负
            this.map2[Math.floor(i/3)][i%3] = value

            this.result()
        },
        //是否分出胜负
        result(){
            const map2 = this.map2
            for(let i=0;i<map2.length;i++){
                 //中间与左右相等 并且不等于null 则赢
                if(map2[i][0] !== null && map2[i][0] === map2[i][1] && map2[i][1] === map2[i][2]){
                    this.res = map2[i][0] + '赢了！'
                    this.isEnd = true
                }else if(map2[0][i] !== null && map2[0][i] === map2[1][i] && map2[1][i] === map2[2][i]){
                    this.res = map2[0][i] + '赢了！'
                    this.isEnd = true
                }else if(map2[0][0] !== null && map2[0][0] === map2[1][1] && map2[1][1] === map2[2][2]){
                    this.res = map2[0][0] + '赢了！'
                    this.isEnd = true
                }else if(map2[0][2] !== null && map2[0][2] === map2[1][1] && map2[1][1] === map2[2][0]){
                    this.res = map2[i][2] + '赢了！'
                    this.isEnd = true
                }
            }
        }
    }
}
</script>

<style scoped>
    .chess-box{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
    .chess-box .chess-item{
        font-size:51px;
        border: 1px solid #000;
        height: 100px;
        width:100px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>