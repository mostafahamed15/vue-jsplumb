<template>  
    <div v-on:mouseleave="update" class="item"  :key="data.label">
        <div id="element1"  class="chart-item" :class="data.shape" :data-key="data.shape">{{data.label}}</div>
    </div>       
</template>
<script>
export default {
    name: 'callaction',
  data() {
    return {
      data: {shape: "rectangle" , label: "Call Action"},
    };
  },
  mounted() {
      
    jsPlumb.ready(function() {
      // All code to initialize Items
      let addaction = jsPlumb.getInstance({
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
      let init = function(connection) {
          console.log(connection);
          connection.getOverlay("label").setLabel("123");
      };
      let addEndpoints = function(toId, sourceAnchors, sourceAnchors1, sourceAnchors2, sourceAnchors3, targetAnchor) {
        console.log(toId, sourceAnchors);
          var sourceUUID = toId + sourceAnchors;
          addaction.addEndpoint(toId, on_answer, {
            anchor: sourceAnchors,
            uuid: sourceUUID
          });

           var sourceUUID1 = toId+ sourceAnchors1;
          addaction.addEndpoint(toId, no_answer, {
            anchor: sourceAnchors1,
            uuid: sourceUUID1
          });

           var sourceUUID2 = toId + sourceAnchors2;
          addaction.addEndpoint(toId, busy, {
            anchor: sourceAnchors2,
            uuid: sourceUUID2
          });

          var sourceUUID3 = toId + sourceAnchors3;
          addaction.addEndpoint(toId, failed, {
            anchor: sourceAnchors3,
            uuid: sourceUUID3
          });

          var targetUUID = toId + targetAnchor;
          addaction.addEndpoint(toId, targetPoint, {
            anchor: targetAnchor,
            uuid: targetUUID
          });
      };
      addaction.batch(function() {
        addaction.bind("connection", function(connInfo, originalEvent) {
          init(connInfo.connection);
        });
    
        addaction.bind("click", function(conn, originalEvent) {
       
        });

        addaction.bind("connectionDrag", function(connection) {
          console.log(
            "connection " +
            connection.id +
            " is being dragged. suspendedElement is ",
            connection.suspendedElement,
            " of type ",
            connection.suspendedElementType
          );
        });

        addaction.bind("connectionDragStop", function(connection) {
          console.log("connection " + connection.id + " was dragged");
        });

        addaction.bind("connectionMoved", function(params) {
          console.log("connection " + params.connection.id + " was moved");
        });
      });
      // 将模块拖入画板中
      $(".box-card .chart-item").draggable({
          scope: "plant",
          helper: "clone",
          containment: $("#work-container")
      });


      $("#workplace").droppable({
          scope: "plant",
          drop: function(ev, ui) {
            console.log(ev, ui);
            let callNumber = '01251421412';
            let cla = "addaction";
            let id = "item" + new Date().getTime();
            let html = `<div id="${id}" class="chart-item  ${ui.helper.attr(
              "data-key"
          )}"><div class="${cla}" ><ul><li>Add Action</li></ul></div>Call ${callNumber}<hr></div>`;
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
              paddingLeft: 15 + "px",
              color: 'blue',
          });
          addEndpoints(
              id,
              "BottomLeft",
              [ .4, 1, 0, 1 ],
              [ .7, 1, 0, 1 ],
              "BottomRight",
              "TopCenter"
          );

          
          addaction.draggable(id, {
              grid: [1, 1]
              // containment: true
          });
        }
      });
      jsPlumb.fire("jsPlumbDemoLoaded", addaction);
    });
  },
   methods: {
 
    update(){
        
      this.$emit('forceRerender1')
    }
  
  }
}

</script>