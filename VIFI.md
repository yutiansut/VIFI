# VIFI协议

## 类型

- 参数说明

  | 参数名称 | 参数说明 | 备注 |
  | -------- | --------| ----- |
  | type | 绘制类型（目前可选：dot/line/area/polygon） | 必填 |
  | data | 数据 | 必填 |

### 打点

- 参数说明

  | 参数名称 | 参数说明                     | 备注 |
  | -------- | ---------------------------- | ---- |
  | Date     | 日期                         | 必填 |
  | Value    | 数值                         | 必填 |
  | Symbol   | svg图标                      | 必填 |
  | Color    | 图标颜色                     | 必填 |
  | Baseline | 图标偏移（0 居中 1 上 2 下） | 必填 |

- 数据格式

  ```
  //一个点
  [{
      type: 'dot',
      data: [
          {
              Date: 20200220,
              Value: 16.5,
              Symbol: '\ue616', // \ue616(买) \ue618（卖）
              Color: 'rgb(240,0,0)',
              Baseline: 0 // 0 居中 1 上 2 下
          }
      ]
  }]
  //多个点
  [{
      type: 'dot',
      data: [
          {
              Date: 20200220,
              Value: 16.5,
              Symbol: '\ue616', // \ue616(买) \ue618（卖）
              Color: 'rgb(240,0,0)',
              Baseline: 0 // 0 居中 1 上 2 下
          },
          {
              Date: 20200318,
              Value: 13.5,
              Symbol: '\ue618', // \ue616(买) \ue618（卖）
              Color: 'rgb(240,240,0)',
              Baseline: 0 // 0 居中 1 上 2 下
          }
      ]
  }]
  ```

### 文字

- 参数说明

  | 参数名称 | 参数说明            | 备注 |
  | -------- | ------------------- | ---- |
  | Date     | 日期                | 必填 |
  | Time     | 时间(分钟K线才有效) | 可选 |
  | Value    | 数值                | 必填 |
  | Color    | 颜色                | 必填 |
  | Text     | 文字                | 必填 |
  | Font     | 字体风格            | 可选 |
  
- 数据格式

  ```javascript
  //绘制单条文字
  [
      {
          type: 'text',
          data: [
              { Date: 20190926, Time: 945, Value: 14.5, Text: '我来试一试', Color: 'rgb(0,255,50)' }
          ]
      }
  ]
  //绘制多条文字
  [
      {
        type: 'text',
          data: [
              { Date: 20190926, Time: 945, Value: 14.5, Text: '我来试一试', Color: 'rgb(0,255,50)' },
              { Date: 20190905, Time: 1425, Value: 14.15, Text: '俺也来', Font: '50px 微软雅黑' }
          ]
      }
  ]
  ```
  
  

### 画线

- 参数说明

  | 参数名称 | 参数说明       | 备注 |
  | -------- | -------------- | ---- |
  | Color    | 颜色           | 必填 |
  | BGColor  | 填充色         | 可选 |
  | Point    | 点坐标数据集合 | 必填 |
  | Date     | 日期           | 必填 |
  | Value    | 数值           | 必填 |


- 数据格式

  ```javascript
  //一条直线
  {
      type: 'line',
      data: [
          {
              Color: 'rgb(255,0,0)',
              BGColor: 'rgba(255,0,0,0.5)',
              Point: [
                  { Date: 20200220, Value: 16.5 },
                  { Date: 20200318, Value: 13.5 }
              ]
          }
      ]
  },
  // 多条直线 
  {
      type: 'line',
      data: [
          {
              Color: 'rgb(255,0,0)', 
              BGColor: 'rgba(255,0,0,0.5)', 
              Point: [
                  { Date: 20200220, Value: 16.5 },
                  { Date: 20200318, Value: 13.5 }
              ]
          },
          {
              Color: 'rgb(255,0,0)',
              BGColor: 'rgba(255,0,0,0.5)',
            	Point: [
                  { Date: 20200220, Value: 13.5 },
                  { Date: 20200318, Value: 16.5 }
              ]
          }
      ]
  },
  ```
  
  

### 面积

- 参数说明

  | 参数名称 | 参数说明                             | 备注 |
  | -------- | ------------------------------------ | ---- |
  | Start    | 开始时间坐标集合                     | 必填 |
  | End      | 开始时间坐标集合                     | 必填 |
  | Color    | 区域颜色                             | 必填 |
  | Date     | 开始日期/结束日期                    | 必填 |
  | Time     | 开始时间/结束时间（仅对分钟K线有效） | 可选 |

- 数据格式

  ```javascript
  //一个区域
  [{
      type: 'area',
      data: [
          {
              Start: { Date: 20200220, Time: null },
              End: { Date: 20200318, Time: null },
              Color: 'rgba(250,128,144,0.5)'
          }
      ]
  }]
  //多个区域
  [{
      type: 'area',
      data: [
          {
            Start: { Date: 20200220, Time: null },
              End: { Date: 20200318, Time: null },
              Color: 'rgba(250,128,144,0.5)'
          },
          {
              Start: { Date: 20191206, Time: null },
              End: { Date: 20200103, Time: null },
              Color: 'rgba(0,255,0,0.5)'
          }
      ]
  }]
  ```
  

### 多边形

- 参数说明

  | 参数名称 | 参数说明       | 备注 |
  | :------- | -------------- | ---- |
  | Color    | 边框颜色       | 必填 |
  | BGColor  | 填充色         | 可选 |
  | Point    | 点坐标数据结合 | 必填 |
  | Date     | 日期           | 必填 |
  | Value    | 数值           | 必填 |

- 注意点

  **坐标要连续（例如绘制矩形：点坐标顺序是：左上点坐标——>右上点坐标——>右下点坐标——>坐下点坐标）**
  
  **只要连续即可（顺时针或逆时针都行）**
  
- 数据格式

  ```javascript
  //绘制一个多边形
  {
      // 至少三个点坐标
      type: 'polygon',
      data: [
          // 例如：矩型
          {
              Color: 'rgba(52,46,37,0)',
              BGColor: 'rgba(255,0,0,0.5)',
              Point: [
                  { Date: 20200108, Value: 16.0 },
                  { Date: 20200213, Value: 16.0 },
                  { Date: 20200213, Value: 14.0 },
                  { Date: 20200108, Value: 14.0 }
              ]
          }
      ]
  }
  //绘制多个多边形
  {
      // 至少三个点坐标
      type: 'polygon',
      data: [
          // 例如：矩型
          {
              Color: 'rgba(52,46,37,0)',
              BGColor: 'rgba(255,0,0,0.5)',
              Point: [
                  { Date: 20200108, Value: 16.0 },
                  { Date: 20200213, Value: 16.0 },
                  { Date: 20200213, Value: 14.0 },
                  { Date: 20200108, Value: 14.0 }
              ]
          },
          // 例如：三角形
          {
              Color: 'rgb(255,0,0)',
              BGColor: 'rgba(255,0,0,0.5)',
              Point: [
                  { Date: 20191022, Value: 17.26 },
                  { Date: 20191113, Value: 15.5 },
                  { Date: 20190925, Value: 15.5 }
              ]
          },
          // 例如:五边形
          {
              Color: 'rgb(255,0,0)',
              BGColor: 'rgba(0,255,0,0.5)',
              Point: [
                  { Date: 20190821, Value: 17.0 },
                  { Date: 20190903, Value: 15.5 },
                  { Date: 20190826, Value: 13.5 },
                  { Date: 20190813, Value: 13.5 },
                  { Date: 20190808, Value: 15.5 }
              ]
          }  
      ]
  }
  ```
  

## 同时绘制多种类型

- 数据格式

  ```javascript
  [
      {
          type: 'dot',
          data: [
              {
                  Date: 20200220,
                  Value: 16.5,
                  Symbol: '\ue616', // \ue616(买) \ue618（卖）
                  Color: 'rgb(240,0,0)',
                  Baseline: 0 // 0 居中 1 上 2 下
              },
              {
                  Date: 20200318,
                  Value: 13.5,
                  Symbol: '\ue618', // \ue616(买) \ue618（卖）
                  Color: 'rgb(240,240,0)',
                  Baseline: 0// 0 居中 1 上 2 下
              }
          ]
      },
      {
          type: 'line',
          data: [
              {
                  Color: 'rgb(255,0,0)', // 直线颜色
                  BGColor: 'rgba(255,0,0,0.5)', // 一条直线这一项可不写
                  Point: [
                      { Date: 20200220, Value: 16.5 },
                      { Date: 20200318, Value: 13.5 }
                  ]
              },
              {
                  Color: 'rgb(255,0,0)', // 直线颜色
                  BGColor: 'rgba(255,0,0,0.5)', // 一条直线这一项可不写
                  Point: [
                      { Date: 20200220, Value: 13.5 },
                      { Date: 20200318, Value: 16.5 }
                  ]
              }
          ]
      },
      {
          type: 'area',
          data: [
              {
                  Start: { Date: 20200220, Time: null },
                  End: { Date: 20200318, Time: null },
                  Color: 'rgba(250,128,144,0.5)'
              },
              {
                Start: { Date: 20191206, Time: null },
                  End: { Date: 20200103, Time: null },
                  Color: 'rgba(0,255,0,0.5)'
              }
          ]
      },
      {
          // 至少三个点坐标
          type: 'polygon',
          data: [
              // 例如：矩型
              {
                  Color: 'rgba(52,46,37,0)',
                  BGColor: 'rgba(255,0,0,0.5)',
                  Point: [
                      { Date: 20200108, Value: 16.0 },
                      { Date: 20200213, Value: 16.0 },
                      { Date: 20200213, Value: 14.0 },
                      { Date: 20200108, Value: 14.0 }
                  ]
              },
              // 例如：三角形
              {
                  Color: 'rgb(255,0,0)',
                  BGColor: 'rgba(255,0,0,0.5)',
                  Point: [
                      { Date: 20191022, Value: 17.26 },
                      { Date: 20191113, Value: 15.5 },
                      { Date: 20190925, Value: 15.5 }
                  ]
              },
              // 例如:五边形
              {
                  Color: 'rgb(255,0,0)',
                  BGColor: 'rgba(0,255,0,0.5)',
                  Point: [
                      { Date: 20190821, Value: 17.0 },
                      { Date: 20190903, Value: 15.5 },
                      { Date: 20190826, Value: 13.5 },
                      { Date: 20190813, Value: 13.5 },
                      { Date: 20190808, Value: 15.5 }
                  ]
              }
          ]
      }
  ]
  ```
  

## 信息地雷

- 参数说明

  | 参数名称    | 参数说明            | 备注 |
  | ----------- | ------------------- | ---- |
  | releasedate | 时间                | 必填 |
  | title       | 信息地雷提示信息    | 必填 |
  | typeex      | 图标（0：买/1：卖） | 必填 |

- 数据格式

  ```
  {
      type:'infoMine',
      data:[
          { releasedate: 20200305, title: '20200305扩展类型公告1', typeex: [0] },
          { releasedate: 20200323, title: '20200323扩展类型公告2', typeex: [1] }
    ]
  }
  ```
  
  