<template>
    <div class="carCharts" v-if="part5B">
        <h3 class="title">员工用车及消费情况</h3>
        <div class="th row">
            <div class="td vmid">员工</div>
            <div class="td vmid">订单量</div>
            <div class="td vmid">占比</div>
            <div class="td vmid">用车金额</div>
            <div class="td vmid">占比</div>
        </div>
        <div class="tr row" v-for="(item, i) in personList" :key="i">
            <div class="td vmid">{{item.name}}</div>
            <div class="td vmid">{{item.orderNum}}</div>
            <div class="td vmid">
                <span class="per">{{item.orderRatePec}}</span>
                <progressGr class="progress" :step="item.orderRate" color="#4780F7"></progressGr>
            </div>
            <div class="td vmid">{{item.orderPrice}}</div>
            <div class="td vmid">
                <span class="per">{{item.orderPriceRatePec}}</span>
                <progressGr class="progress" :step="item.orderPriceRate" color="#EDAC4A"></progressGr>
            </div>
        </div>
        <div class="empty" v-if="personList.length <= 0">
            <img src="@/static/images/home_img_empty.svg">
            <p class="emTxt">暂无数据</p>
        </div>
    </div>
</template>

<script>
import progressGr from "@/commonComponents/baseProgress";
import _ from "lodash";

export default {
    name: "homepart5",
    props: ["data"],
    components: {
        progressGr,
    },
    data() {
        return {
            personList: [],
        }
    },
    watch: {
        data: {
            immediate: true,
            handler(val) {
                let list = _.cloneDeep(val) || [];
                list.map(e => {
                    e.orderRatePec = ~~(e.orderRate * 100) + "%";
                    e.orderPriceRatePec = ~~(e.orderPriceRate * 100) + "%";
                });
                this.personList = list;
            }
        }
    },
    computed: {
        part5B() {
            return this.data && this.data.orderView;
        }
    },
}
</script>

<style lang="scss" scoped>
.carCharts {
    background: #fff;
    padding: 20px 24px 24px 24px;
    .title {
        font-size: 16px;
        color: #000;
        font-weight: 600;
        line-height: 23px;
    }
    .row {
        white-space: nowrap;
    }
    .th {
        line-height: 20px;
        padding: 20px 0 15px 0;
        border-bottom: 1px solid #f5f5f5;
        .td {
            color: #4A4A4A;
            font-size: 14px;
            font-weight: 600;
        }
    }
    .tr {
        line-height: 20px;
        padding: 10px 0;
        border-bottom: 1px solid #f5f5f5;
        .td {
            color: #888;
            font-size: 14px;
        }
    }
    .td {
        width: calc(20% - 5px);
        .per {
            margin-right: 6px;
            display: inline-block;
            vertical-align: middle;
        }
        .progress {
            width: 120px;
        }
    }
    .empty {
        text-align: center;
        padding: 40px 0;
        .emTxt {
            color: #888;
            font-size: 14px;
        }
    }
}
</style>
