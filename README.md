# Hello-word
Just a test
这是我学习的封装函数
function Bubble(arr){
    for(var i = 0;i < arr.length;i++){ //冒泡排序
        for(var j = 0;j < arr.length-i-1;j++){
            if(arr[j] > arr[j+1]){
                var tmp = arr[j+1];
                arr[j+1] = arr[j];
                arr[j] = tmp;
            }
        }
    }
    return arr;      
}


function Choose(arr){
    for(var i=0;i<arr.length-1;i++){ //选择排序
        for(var j=i+1;j<arr.length;j++){
            if(arr[i]>arr[j]){
                var tmp=arr[j];
                arr[j]=arr[i];
                arr[i]=tmp;
            }
        }
    }
    return arr;
}
function getStyle(elem, attr){  //获取当前样式
    return elem.currentStyle ? elem.currentStyle[attr] : getComputedStyle(elem)[attr];
}



function elementByClassName(parent, oclass){  //封装函数  解决ByclassName的IE兼容问题
    var num = parent.getElementsByTagName("*");
    var result = [];
    for(var i = 0; i < num.length; i++){
        if(num[i].className == oclass){
            result.push(num[i]);
        }
    }
    return result;
}




function $(vArg){ //获取元素节点函数
    switch(vArg[0]){
        case "#": //id
             return document.getElementById(vArg.substring(1));
             break;
        case ".": //class
            return elementByClassName(document,vArg.substring(1));
            break;
        default:
            var str = vArg.substring(0,5);
            if(str == "name="){
                return document.getElementsByName(vArg.substring(5));
            }else{
                return document.getElementsByTagName(vArg);
            }
            break;
    }
}


function judgeSpaceNodes(node){
    var result = [];
    for(var i =node.length - 1 ; i >= 0; i--){
        if(node[i].nodeType == 3 && /^\s+$/.test(node[i].nodeValue)){
            continue; //判断为空节点则不做操作 继续执行循环
        }else{
            result.push(node[i]); //把不是空节点插入数组中
        }
    }
    return result;
}



function removeSpaceNodes(parent){ //必须从父节点上删除空白节点 
    var nodes = parent.childNodes;
    for(var i =nodes.length - 1 ; i >= 0; i--){
        if(nodes[i].nodeType == 3 && /^\s+$/.test(nodes[i].nodeValue)){
            parent.removeChild(nodes[i]);
        }
    }
}


function createElementWithTextNode(elem, values){  //创建一个带文本的元素节点并插入
    var nodes = document.createElement(elem);
    var otext = document.createTextNode(values);
    nodes.appendChild(otext);
    return nodes;
}



function insertAfter(newNode, oldNode){  //在目标节点之后插入节点
    var parent = oldNode.parentNode;
    if(oldNode == parent.lastChild){
        parent.appendChild(newNode);
    }else{
        parent.insertBefore(newNode, oldNode.nextSibling);
    }

} 
