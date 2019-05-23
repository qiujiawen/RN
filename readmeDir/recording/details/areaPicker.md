# 行政区选择器

使用的是《中华人民共和国行政区划代码》国家标准(GB/T2260)，也就是2016年的国家标准行政区。代码中使用的数据：[行政区数据](./area.js)

```
import React from "react";
import {Text, TouchableOpacity, View, StyleSheet} from "react-native";
import {SCREEN_HEIGHT, SCREEN_WIDTH, setScreenSizeHeight, setScreenSizeWidth, setFontSize} from "../../global";
import {Provider, PickerView} from "@ant-design/react-native";
import districtData from '../../data/area';

export default class AreaPicker extends React.Component {

    state = {
        pickerValue: [],    // 选择器的值
    };

    // 点击完成的事件处理
    _completeHandle = ()=>{

        let strArea = '';
        if (this.state.pickerValue.length == 0){
            strArea = '北京市 北京市';
        }else {
            let arr = this.state.pickerValue.filter((item,index)=>{
                if (index == 2){
                    return false;
                } else {
                    return item;
                }
            });
            strArea = arr.join(' ');
        }
        this.props.areaPickerHandle(strArea);
    };

    render() {

        //  对原始数据整合
        let areaData =[];
        
        Object.keys(districtData).forEach((index)=>{
                    let itemLevel1 ={};
                    let itemLevel2 ={};
                    itemLevel1.value = districtData[index].code;
                    itemLevel1.label = districtData[index].name;
                    itemLevel1.children = [];
                    let data = districtData[index].cities;
                    Object.keys(data).forEach((index)=>{
                        itemLevel2.value = data[index].code;
                        itemLevel2.label = data[index].name;
                        itemLevel2.children = [];
                        let data2 = data[index].districts;
                        let itemLevel3 ={};
                        itemLevel3.children = [];
                        Object.keys(data2).forEach((index)=>{
                            itemLevel3.value = index;
                            itemLevel3.label = data2[index];
                            itemLevel2.children.push(itemLevel3);
                            itemLevel3 ={};
                        });
                        itemLevel1.children.push(itemLevel2);
                        itemLevel2 ={};
                    });
                    areaData.push(itemLevel1)
                });

        return (
            <View style={style.dateWrap}>

                <View style={style.headerView}></View>

                <View style={style.buttonWrap}>

                    <TouchableOpacity
                        onPress={() => this.props.areaPickerHandle(this.props.areaStr)}
                        activeOpacity={1}
                    >
                        <Text style={style.cancel}>取消</Text>
                    </TouchableOpacity>

                    <TouchableOpacity
                        onPress={this._completeHandle}
                        activeOpacity={1}
                    >
                        <Text style={style.complete}>完成</Text>
                    </TouchableOpacity>

                </View>

                <View style={style.pickerWrap}>
                    <Provider>
                        <PickerView
                            data={areaData}
                            cols={3}
                            value={this.state.pickerValue}
                            onChange={v => this.setState({ pickerValue: v })}
                        />
                    </Provider>
                </View>

            </View>
        );
    }
}

const style = StyleSheet.create({

    // 视图的样式
    dateWrap: {
        width: SCREEN_WIDTH,
        height: SCREEN_HEIGHT,
        zIndex: 10,
        position: 'absolute',
        top: 0,
        left: 0
    },

    // 阴影部分视图
    headerView: {
        backgroundColor: 'rgba(32,32,32,0.65)',
        height: setScreenSizeHeight(702),
    },

    //  取消、完成的样式
    buttonWrap: {
        width: SCREEN_WIDTH,
        height: setScreenSizeHeight(87),
        flexDirection: 'row',
        justifyContent: 'space-between',
        alignItems: 'center',
        backgroundColor: '#fff',
        borderBottomWidth: 1,
        borderStyle: 'solid',
        borderBottomColor: '#e5e5e5'
    },

    //  取消按钮的样式
    cancel: {
        color: '#1e82d2',
        marginLeft: setScreenSizeWidth(30),
        fontSize: setFontSize(30),
        fontWeight: "500"
    },

    //  完成按钮的样式
    complete: {
        color: '#1e82d2',
        marginRight: setScreenSizeWidth(30),
        fontSize: setFontSize(30),
        fontWeight: '500'
    },

    //  选择器的样式
    pickerWrap: {
        width: SCREEN_WIDTH,
        height: SCREEN_HEIGHT - setScreenSizeHeight(789),
        backgroundColor: '#fff'
    },

});

```