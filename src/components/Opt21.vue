<template>
    <el-container class="container" id="work-container">
      <el-aside width="200px">
        <div class="box-card">
            <div class="header">Actions</div>
            <div class="card-body">
            <div  class="item"  :key="start.label">
                <div   class="chart-item" :class="start.shape" :data-key="start.shape">{{start.label}}</div>
            </div>
            <div  class="item"  :key="callAction.label">
                <div   class="chart-item" :class="callAction.shape" :data-key="callAction.shape">{{callAction.label}}</div>
            </div>
            <div  class="item"  :key="playSoundAction.label">
                <div   class="chart-item" :class="playSoundAction.shape" :data-key="playSoundAction.shape">{{playSoundAction.label}}</div>
            </div>
            <div  class="item"  :key="callInputAction.label">
                <div  class="chart-item" :class="callInputAction.shape" :data-key="callInputAction.shape">{{callInputAction.label}}</div>
            </div>
            </div>
        </div>
      </el-aside>
      <el-main>
        <div class="workplace" id="workplace">
          </div>
      
      </el-main>
    </el-container>
</template>
<script>
export default {
  data() {
    return {
      start: {shape: "rectangle" , label: "Start"},
      callAction: {shape: "rectangle" , label: "Call Action"},
      playSoundAction: {shape: "rectangle" , label: "Play Sound Action"},
      callInputAction: {shape: "rectangle" , label: "Call Input Action"}
    };
  },
  mounted() {
    jsPlumb.ready(function() {
      // All code to initialize Items
      let instance = jsPlumb.getInstance({
        Connector:"StateMachine", Endpoint:["Dot", {radius:3}],
        // drag options
        DragOptions: { cursor: "pointer", zIndex: 2000 },
        // overlays
        ConnectionOverlays: [
          [
              "Arrow",
              {
                location: 1,
                visible: true,
                width: 11,
                height: 11,
                id: "Arrow"
              }
          ],
          [
            "Label",
              {
                label: "Connect",
                location: 0.2,
                id: "Label",
                cssClass: "arrow-label",
                events: {
                  tap() {
                    console.log("Label");
                  }
                }
              }
          ]
        ],
        Container: "workplace"
      });
      
      // 连接线默认样式
      let connectorPaintStyle = {
        strokeWidth: 2,
        stroke: "#61B7CF",
        joinstyle: "round",
        outlineStroke: "white",
        outlineWidth: 2
      };
      // hover style.
      let connectorHoverStyle = {
        strokeWidth: 3,
        stroke: "#216477",
        outlineWidth: 5,
        outlineStroke: "white"
      };
      let endpointHoverStyle = {
        fill: "#216477",
        stroke: "#216477"
      };
      // source endpoints
      let sourceEndpoint = {
        endpoint: "Dot",
        paintStyle: {
          stroke: "#7AB02C",
          fill: "transparent",
          radius: 7,
          strokeWidth: 1
        },
        isSource: true,
        connector: [
          "Flowchart",
            {
              stub: [40, 60],
              gap: 10,
              cornerRadius: 5,
              alwaysRespectStubs: true
            }
        ],
        connectorStyle: connectorPaintStyle,
        hoverPaintStyle: endpointHoverStyle,
        connectorHoverStyle: connectorHoverStyle,
        dragOptions: {},
        overlays: [
          [
            "Label",
              {
                location: [3.5, -.4],
                label: "Incoming SMS",
                cssClass: "endpointSourceLabel",
                visible: true
              }
          ]
        ]
      };

      // source endpoints
      let sourceEndpoint1 = {
        endpoint: "Dot",
        paintStyle: {
          stroke: "#7AB02C",
          fill: "transparent",
          radius: 7,
          strokeWidth: 1
        },
        isSource: true,
        connector: [
          "Flowchart",
            {
              stub: [40, 60],
              gap: 10,
              cornerRadius: 5,
              alwaysRespectStubs: true
            }
        ],
        connectorStyle: connectorPaintStyle,
        hoverPaintStyle: endpointHoverStyle,
        connectorHoverStyle: connectorHoverStyle,
        dragOptions: {},
        overlays: [
          [
            "Label",
              {
                location: [0.5, -.4],
                label: "Incoming Call",
                cssClass: "endpointSourceLabel",
                visible: true
              }
          ]
        ]
      };

      // source endpoints
      let sourceEndpoint2 = {
        endpoint: "Dot",
        paintStyle: {
          stroke: "#7AB02C",
          fill: "transparent",
          radius: 7,
          strokeWidth: 1
        },
        isSource: true,
        connector: [
          "Flowchart",
            {
              stub: [40, 60],
              gap: 10,
              cornerRadius: 5,
              alwaysRespectStubs: true
            }
        ],
        connectorStyle: connectorPaintStyle,
        hoverPaintStyle: endpointHoverStyle,
        connectorHoverStyle: connectorHoverStyle,
        dragOptions: {},
        overlays: [
          [
            "Label",
              {
                location: [-2.5, -.4],
                label: "API Request",
                cssClass: "endpointSourceLabel",
                visible: true
              }
          ]
        ]
      };
      // target endpoints
      let targetEndpoint = {
        endpoint: "Dot",
        paintStyle: { fill: "#7AB02C", radius: 7 },
        hoverPaintStyle: endpointHoverStyle,
        maxConnections: -1,
        dropOptions: { hoverClass: "hover", activeClass: "active" },
        isTarget: true,
        overlays: [
          [
            "Label",
            {
              location: [0.5, -0.5],
              label: "Drop",
              cssClass: "endpointTargetLabel",
              visible: true
            }
          ]
        ]
      };

       // source endpoints
      let on_answer = {
        endpoint: "Dot",
        paintStyle: {
          stroke: "#7AB02C",
          fill: "transparent",
          radius: 7,
          strokeWidth: 1
        },
        isSource: true,
        connector: [
          "Flowchart",
            {
              stub: [40, 60],
              gap: 10,
              cornerRadius: 5,
              alwaysRespectStubs: true
            }
        ],
        connectorStyle: connectorPaintStyle,
        hoverPaintStyle: endpointHoverStyle,
        connectorHoverStyle: connectorHoverStyle,
        dragOptions: {},
        overlays: [
          [
            "Label",
              {
                location: [3, -.4],
                label: "On Answer",
                cssClass: "endpointSourceLabel",
                visible: true
              }
          ]
        ]
      };

      // source endpoints
      let no_answer = {
        endpoint: "Dot",
        paintStyle: {
          stroke: "#7AB02C",
          fill: "transparent",
          radius: 7,
          strokeWidth: 1
        },
        isSource: true,
        connector: [
          "Flowchart",
            {
              stub: [40, 60],
              gap: 10,
              cornerRadius: 5,
              alwaysRespectStubs: true
            }
        ],
        connectorStyle: connectorPaintStyle,
        hoverPaintStyle: endpointHoverStyle,
        connectorHoverStyle: connectorHoverStyle,
        dragOptions: {},
        overlays: [
          [
            "Label",
              {
                location: [1, -.4],
                label: "No Answer",
                cssClass: "endpointSourceLabel",
                visible: true
              }
          ]
        ]
      };

       let busy = {
        endpoint: "Dot",
        paintStyle: {
          stroke: "#7AB02C",
          fill: "transparent",
          radius: 7,
          strokeWidth: 1
        },
        isSource: true,
        connector: [
          "Flowchart",
            {
              stub: [40, 60],
              gap: 10,
              cornerRadius: 5,
              alwaysRespectStubs: true
            }
        ],
        connectorStyle: connectorPaintStyle,
        hoverPaintStyle: endpointHoverStyle,
        connectorHoverStyle: connectorHoverStyle,
        dragOptions: {},
        overlays: [
          [
            "Label",
              {
                location: [1, -.4],
                label: "Busy",
                cssClass: "endpointSourceLabel",
                visible: true
              }
          ]
        ]
      };

       let failed = {
        endpoint: "Dot",
        paintStyle: {
          stroke: "#7AB02C",
          fill: "transparent",
          radius: 7,
          strokeWidth: 1
        },
        isSource: true,
        connector: [
          "Flowchart",
            {
              stub: [40, 60],
              gap: 10,
              cornerRadius: 5,
              alwaysRespectStubs: true
            }
        ],
        connectorStyle: connectorPaintStyle,
        hoverPaintStyle: endpointHoverStyle,
        connectorHoverStyle: connectorHoverStyle,
        dragOptions: {},
        overlays: [
          [
            "Label",
              {
                location: [-1, -.4],
                label: "Failed",
                cssClass: "endpointSourceLabel",
                visible: true
              }
          ]
        ]
      };

       let targetPoint = {
       endpoint: "Dot",
        paintStyle: { fill: "#7AB02C", radius: 7 },
        hoverPaintStyle: endpointHoverStyle,
        maxConnections: -1,
        dropOptions: { hoverClass: "hover", activeClass: "active" },
        isTarget: true,
        overlays: [
          [
            "Label",
            {
              location: [0.5, -0.5],
              label: "Drop",
              cssClass: "endpointTargetLabel",
              visible: false
            }
          ]
        ]
      };

       let targetPoint2 = {
       endpoint: "Dot",
        paintStyle: { fill: "#7AB02C", radius: 7 },
        hoverPaintStyle: endpointHoverStyle,
        maxConnections: -1,
        dropOptions: { hoverClass: "hover", activeClass: "active" },
        isTarget: true,
        overlays: [
          [
            "Label",
            {
              location: [0.5, -0.5],
              label: "Drop",
              cssClass: "endpointTargetLabel",
              visible: false
            }
          ]
        ]
      };
      let init = function(connection) {
          console.log(connection);
          connection.getOverlay("label").setLabel("123");
      };
     
       let addEndpoints1 = function(toId, sourceAnchors, sourceAnchors1, sourceAnchors2, sourceAnchors3, targetAnchor) {
        console.log(toId, sourceAnchors);
          var sourceUUID3 = toId + sourceAnchors;
          instance.addEndpoint(toId, on_answer, {
            anchor: sourceAnchors,
            uuid: sourceUUID3
          });

           var sourceUUID4 = toId+ sourceAnchors1;
          instance.addEndpoint(toId, no_answer, {
            anchor: sourceAnchors1,
            uuid: sourceUUID4
          });

           var sourceUUID5 = toId + sourceAnchors2;
          instance.addEndpoint(toId, busy, {
            anchor: sourceAnchors2,
            uuid: sourceUUID5
          });

          var sourceUUID6 = toId + sourceAnchors3;
          instance.addEndpoint(toId, failed, {
            anchor: sourceAnchors3,
            uuid: sourceUUID6
          });

          var targetUUID = toId + targetAnchor;
          instance.addEndpoint(toId, targetPoint, {
            anchor: targetAnchor,
            uuid: targetUUID
          });
      };

       let addEndpoints2 = function(toId, targetAnchors) {
        console.log(toId, targetAnchors);
          var targetUUID = toId + targetAnchors;
          instance.addEndpoint(toId, targetPoint2, {
            anchor: targetAnchors,
            uuid: targetUUID
          });
      };

      // 暂停渲染，执行以下操作
      instance.batch(function() {
        // listen for new connections;
        instance.bind("connection", function(connInfo, originalEvent) {
          init(connInfo.connection);
        });
        /* // make all the window divs draggable
        instance.draggable($(".workplace .chart-item"), {
        grid: [1, 1]
        }); */

        // listen for clicks on connections, and offer to delete connections on click.
        instance.bind("click", function(conn, originalEvent) {
        // if (confirm("Delete connection from " + conn.sourceId + " to " + conn.targetId + "?"))
        //   instance.detach(conn);
        // conn.toggleType("basic");
        });

        instance.bind("connectionDrag", function(connection) {
          console.log(
            "connection " +
            connection.id +
            " is being dragged. suspendedElement is ",
            connection.suspendedElement,
            " of type ",
            connection.suspendedElementType
          );
        });

        instance.bind("connectionDragStop", function(connection) {
          console.log("connection " + connection.id + " was dragged");
        });

        instance.bind("connectionMoved", function(params) {
          console.log("connection " + params.connection.id + " was moved");
        });
      });
      // 将模块拖入画板中
      $(".box-card .chart-item").draggable({
          scope: "plant",
          helper: "clone",
          containment: $("#work-container")
      });

    //    $(".box-card .chart-item1").draggable({
    //       scope: "plant",
    //       helper: "clone",
    //       containment: $("#work-container")
    //   });
      $("#workplace").droppable({
          scope: "plant",
          drop: function(ev, ui) {
            console.log(ev, ui, ui.draggable[0].classList);
            var text = ui.helper[0].childNodes[0].data;
            console.log(text)
          if (text) {
              switch (text){
              case 'Start':
                  let startPhrase = "PHILO excution will start from this page";
            let cla = "start";
            let id = "item" + new Date().getTime();
            let html = `<div id="${id}" class="chart-item  ${ui.helper.attr(
              "data-key"
          )}"><div class="${cla}" ><ul><li>Start</li></ul></div>${startPhrase}<hr></div>`;
          $(this).append(html);
          $("#" + id).css({
              width: 300 + "px",
              height: 90 + "px",
              top: ui.position.top -20 + "px",
              left: ui.position.left - 460 + "px",
              background: 'white',
              border: 1 + 'px' + ' solid' + ' red',
          });
          $("." + cla).css({
              border: 1 + 'px' + ' solid' + ' red', 
              textAlign: 'left',
              paddingLeft: 15 + "px"
          });

           let addEndpoints = function(toId, sourceAnchors, sourceAnchors1, sourceAnchors2) {
        console.log(toId, sourceAnchors);
       // for (var i = 0; i < sourceAnchors.length; i++) {
          var sourceUUID = toId + sourceAnchors;
          instance.addEndpoint(toId, sourceEndpoint, {
            anchor: sourceAnchors,
            uuid: sourceUUID
          });

           var sourceUUID1 = toId+ sourceAnchors1;
          instance.addEndpoint(toId, sourceEndpoint1, {
            anchor: sourceAnchors1,
            uuid: sourceUUID1
          });

           var sourceUUID2 = toId + sourceAnchors2;
          instance.addEndpoint(toId, sourceEndpoint2, {
            anchor: sourceAnchors2,
            uuid: sourceUUID2
          });
       // }
        // for (var j = 0; j < targetAnchors.length; j++) {
        //   var targetUUID = toId + targetAnchors[j];
        //   start.addEndpoint(toId, targetEndpoint, {
        //     anchor: targetAnchors[j],
        //     // anchor: 'Continuous',
        //     uuid: targetUUID
        //   });
        // }
      };

          addEndpoints(
              id,
              "BottomLeft",
              "BottomCenter",
              "BottomRight"
          );

          
          instance.draggable(id, {
              grid: [1, 1],
               //containment: true
          });
          
          break; 
          case "Call Action":
           let callNumber = '01251421412';
            let clas = "addaction";
            let id1 = "item" + new Date().getTime();
            let html1 = `<div id="${id1}" class="chart-item  ${ui.helper.attr(
              "data-key"
          )}"><div class="${clas}" ><ul><li>Add Action</li></ul></div>Call ${callNumber}<hr></div>`;
          $(this).append(html1);
          $("#" + id1).css({
              width: 300 + "px",
              height: 90 + "px",
              top: ui.position.top -20 + "px",
              left: ui.position.left - 460 + "px",
              background: 'white',
              border: 1 + 'px' + ' solid' + ' red',
          });
          $("." + clas).css({
              border: 1 + 'px' + ' solid' + ' red', 
              textAlign: 'left',
              paddingLeft: 15 + "px",
              color: 'blue',
          });
          addEndpoints1(
              id1,
              "BottomLeft",
              [ .4, 1, 0, 1 ],
              [ .7, 1, 0, 1 ],
              "BottomRight",
              "TopCenter"
          );

          
          instance.draggable(id1, {
              grid: [1, 1]
              // containment: true
          });
          break;
          case "Play Sound Action" :
               let url = "https://glocum.com";
            let clas1 = "start";
            let id2 = "item" + new Date().getTime();
            let html2 = `<div id="${id2}" class="chart-item  ${ui.helper.attr(
              "data-key"
          )}"><div class="${clas1}" ><ul><li>Play Sound Action</li></ul></div>${url}<hr></div>`;
          $(this).append(html2);
          $("#" + id2).css({
              width: 300 + "px",
              height: 90 + "px",
              top: ui.position.top -20 + "px",
              left: ui.position.left - 460 + "px",
              background: 'white',
              border: 1 + 'px' + ' solid' + ' red',
          });
          $("." + clas1).css({
              border: 1 + 'px' + ' solid' + ' red', 
              textAlign: 'left',
              paddingLeft: 15 + "px"
          });
          addEndpoints2(
              id2,
              "TopCenter"
          );
          instance.draggable(id2,{
              grid: [1, 1]
              // containment: true
          });
          break;

          case "Call Input Action" :
            let userInput = 'Get User Input and evaluate if input is either 1, 2';
            let cla3 = "callInputAction";
            let id3 = "item" + new Date().getTime();
            let html3 = `<div id="${id3}" class="chart-item  ${ui.helper.attr(
              "data-key"
          )}"><div class="${cla3}" ><ul><li>Call Input Action</li></ul></div>${userInput}<hr></div>`;
          $(this).append(html3);
          $("#" + id3).css({
              width: 300 + "px",
              height: 90 + "px",
              top: ui.position.top -20 + "px",
              left: ui.position.left - 460 + "px",
              background: 'white',
              border: 1 + 'px' + ' solid' + ' red',
          });
          $("." + cla3).css({
              border: 1 + 'px' + ' solid' + ' red', 
              textAlign: 'left',
              paddingLeft: 15 + "px",
              color: 'blue',
          });

          let addEndpoints3 = function(toId, sourceAnchors, sourceAnchors1, sourceAnchors2, sourceAnchors3, targetAnchor) {
        console.log(toId, sourceAnchors);
          var sourceUUID = toId + sourceAnchors;
          instance.addEndpoint(toId, on_answer, {
            anchor: sourceAnchors,
            uuid: sourceUUID
          });

           var sourceUUID1 = toId+ sourceAnchors1;
          instance.addEndpoint(toId, no_answer, {
            anchor: sourceAnchors1,
            uuid: sourceUUID1
          });

           var sourceUUID2 = toId + sourceAnchors2;
          instance.addEndpoint(toId, busy, {
            anchor: sourceAnchors2,
            uuid: sourceUUID2
          });

          var sourceUUID3 = toId + sourceAnchors3;
          instance.addEndpoint(toId, failed, {
            anchor: sourceAnchors3,
            uuid: sourceUUID3
          });

          var targetUUID = toId + targetAnchor;
          instance.addEndpoint(toId, targetPoint, {
            anchor: targetAnchor,
            uuid: targetUUID
          });
      };
          addEndpoints3(
              id3,
              "BottomLeft",
              [ .4, 1, 0, 1 ],
              [ .7, 1, 0, 1 ],
              "BottomRight",
              "TopCenter"
          );

          
          instance.draggable(id3, {
              grid: [1, 1]
              // containment: true
          });
            break;
              } 
          }
        }
      });

      

      
      //       j.bind("connection", function(p) {
      //           p.connection.bind("click", function() {
      //               j.detach(this);
      //           });
      //       });

      //       var evts = document.querySelector("#events");
      //       var _appendEvent = function(name, detail) {
      //           evts.innerHTML = "<br/><strong>" + name + "</strong><br/> " + detail + "<br/>" + evts.innerHTML;
      //       };
      //       j.bind("group:addMember", function(p) {
      //           _appendEvent("group:addMember", p.group.id + " - " + p.el.id);
      //       });
      //       j.bind("group:removeMember", function(p) {
      //           _appendEvent("group:removeMember", p.group.id + " - " + p.el.id);
      //       });
      //       j.bind("group:expand", function(p) {
      //           _appendEvent("group:expand", p.group.id);
      //       });
      //       j.bind("group:collapse", function(p) {
      //           _appendEvent("group:collapse", p.group.id);
      //       });
      //       j.bind("group:add", function(p) {
      //           _appendEvent("group:add", p.group.id);
      //       });
      //       j.bind("group:remove", function(p) {
      //           _appendEvent("group:remove", p.group.id);
      //       });

      //       // connect some before configuring group
       //      instance.connect({source:c1_1, target:c2_1});
      //       j.connect({source:c2_1, target:c3_1});
      //       j.connect({source:c2_2, target:c6_2});
      //       j.connect({source:c3_1, target:c4_1});
      //       j.connect({source:c4_1, target:c5_1});
        //     instance.connect({source:c1_1,target:c1_2});
      //       j.connect({source:c2_1,target:c2_2});

      //       // NOTE ordering here. we make one draggable before adding it to the group, and we add the other to the group
      //       //before making it draggable. they should both be constrained to the group extents.
      //       j.draggable(c1_1);
            // instance.addGroup({
            //     el:container1,
            //     id:"one",
            //     constrain:true,
            //     anchor:"Continuous",
            //     endpoint:"Blank",
            //     droppable:true
            // });
            // instance.addToGroup("one", c1_1);
            // instance.addToGroup("one", c1_2);
            // instance.addToGroup("one", c1_3);
      //       j.draggable(c1_2);


      //       j.draggable(c2_1);
      //       j.addGroup({
      //           el:container2,
      //           id:"two",
      //           dropOverride:true,
      //           endpoint:["Dot", { radius:3 }]
      //       });  //(the default is to revert)
      //       j.addToGroup("two", c2_1);
      //       j.addToGroup("two", c2_2);
      //       j.draggable(c2_2);

      //       j.draggable(c3_1);
      //       j.addGroup({
      //           el:container3,
      //           id:"three",
      //           revert:false,
      //           endpoint:["Dot", { radius:3 }]
      //       });
      //       j.addToGroup("three", c3_1);
      //       j.addToGroup("three", c3_2);
      //       j.draggable(c3_2);

      //       j.draggable(c4_1);
      //       j.addGroup({
      //           el:container4,
      //           id:"four",
      //           prune:true,
      //           endpoint:["Dot", { radius:3 }]
      //       });
      //       j.addToGroup("four", c4_1);
      //       j.addToGroup("four", c4_2);
      //       j.draggable(c4_2);

      //       j.draggable(c5_1);
      //       j.addGroup({
      //           el:container5,
      //           id:"five",
      //           orphan:true,
      //           droppable:false,
      //           endpoint:["Dot", { radius:3 }]
      //       });
      //       j.addToGroup("five", [c5_1, c5_2]);
      //       j.draggable(c5_2);

      //       j.draggable(c6_1);
      //       j.addGroup({
      //           el:container6,
      //           id:"six",
      //           proxied:false,
      //           endpoint:["Dot", { radius:3 }]
      //       });
      //       j.addToGroup("six", [c6_1, c6_2]);
      //       j.draggable(c6_2);

      //       j.draggable(c7_1);
      //       j.addGroup({
      //           el:container7,
      //           id:"seven",
      //           ghost:true,
      //           endpoint:["Dot", { radius:3 }]
      //       });
      //       j.addToGroup("seven", [c7_1, c7_2]);
      //       j.draggable(c7_2);

      //       // the independent element that demonstrates the fact that it can be dropped onto a group
      //       j.draggable("standalone");

      //       //... and connect others afterwards.
      //       j.connect({source:c3_1,target:c3_2});
      //       j.connect({source:c4_1,target:c4_2});
      //       j.connect({source:c5_1,target:c5_2});
      //       j.connect({source:c5_1,target:c3_2});
      //       j.connect({source:c5_1,target:container5, anchors:["Center", "Continuous"]});
      //       j.connect({source:c5_2,target:c6_1});
      //       j.connect({source:c6_2,target:c7_1});

            // delete group button
            // instance.on(canvas, "click", ".del", function() {
            //     var g = this.parentNode.getAttribute("group");
            //     instance.removeGroup(g, this.getAttribute("delete-all") != null);
            // });


      //       // collapse/expand group button
      //       j.on(canvas, "click", ".node-collapse", function() {
      //           var g = this.parentNode.getAttribute("group"), collapsed = j.hasClass(this.parentNode, "collapsed");

      //           j[collapsed ? "removeClass" : "addClass"](this.parentNode, "collapsed");
      //           j[collapsed ? "expandGroup" : "collapseGroup"](g);
      //       });
      jsPlumb.fire("jsPlumbDemoLoaded", instance);
    });
  }
}
</script>
<style scoped>
.el-aside {
    background-color: #D3DCE6;
    color: #333;
}
.workplace {
  width: 100%;
  height: 100%;
  position: relative;
}

.w {
    position:absolute;
    height:30px;
    border:1px solid black;
    font-size:12px;
    border-radius:3px;
    text-align:center;
    background-color:WhiteSmoke;
    opacity:0.7;
    z-index:10;
    color:black;
    cursor:move;
}

.w:hover {
    background-color:#629f8d;
}

.group-container {
    position: absolute;
    width: 230px;
    height: 100px;
    border-radius: 12px;
    background-color: WhiteSmoke;
    font-size: 12px;
    cursor:move;
}

.group-container ul {
    margin-left:25px;
    padding: 0;
}



.large {
    width:600px;
    height:600px;
}

.group-container.collapsed {
    height:40px;
}

.title {
    background-color:#ABC1BB;
    padding-right:16px;
    font-size:13px;
    height:30px;
}

#container1 { left:20px;top:50px; }
#container2 { left:250px;top:50px; }
#container3 { left:480px;top:50px; }
#container4 { left:710px;top:50px; }
#container5 { left:600px;top:340px; }
#container6 { left:370px;top:340px; }
#container7 { left:140px;top:340px; }

.del, .node-collapse {
    position:absolute;
    top:5px;
    right:5px;
    background-color:white;
    padding:1px;
    cursor:pointer;
    font-size:13px;
    width:20px;
    height:20px;
    border-radius: 50%;
    text-align:center;
    display:block;
}

.del:after {
    content:"X";
}

.node-collapse {
    right:29px;
    text-align: center;
}

.node-collapse:after {
    content:"-";
}

.group-container.collapsed .node-collapse:after {
    content:"+";
}

.del[delete-all] {
    background-color: pink;
}

.jtk-connector path {
    stroke-width:1;
}

.jtk-group-collapsed .w, .jtk-group-collapsed ul, .jtk-group-collapsed .container, .jtk-group-collapsed .name {
    display:none;
}

.jtk-drag-hover {
    outline:4px solid cornflowerblue;
}

.katavorio-ghost-proxy {
    outline:2px solid red;
}

.events {
    position:absolute;
    right:0;
    top:0;
    border-left:4px solid #58775d;
    bottom:0;
    width:156px;
    font-size: 11px;
    padding-left:11px;
    background-color: white;
}

#events {
    position: absolute;
    right: 0;
    top: 0;
    border-left: 1px solid #58775d;
    bottom: 0;
    width: 256px;
    font-size: 11px;
    padding-left: 11px;
    background-color: white;
}

.events h3 {
    font-size: 20px;
    margin-top: 10px;
}
.title-word {
  list-style: none;
  padding-top: 9px !important;
}

.title-word li::before {
  content: "\2022";
  color: red;
  font-weight: bold;
  display: inline-block; 
  width: 1em;
  margin-left: -1em;
}


</style>