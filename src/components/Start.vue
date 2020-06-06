<template>  
    <div v-on:mouseleave="update"  class="item"  :key="data.label">
        <div   class="chart-item" :class="data.shape" :data-key="data.shape">{{data.label}}</div>
    </div>       
</template>
<script>
export default {
    name: 'start',
    props: ['user'],
  data() {
    return {
      data: {shape: "rectangle" , label: "Start"},
    };
  },
  mounted() {
    jsPlumb.ready(function() {
      // All code to initialize Items
      let start = jsPlumb.getInstance({
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
      let init = function(connection) {
          console.log(connection);
          connection.getOverlay("label").setLabel("123");
      };
      let addEndpoints = function(toId, sourceAnchors, sourceAnchors1, sourceAnchors2) {
        console.log(toId, sourceAnchors);
          var sourceUUID = toId + sourceAnchors;
          start.addEndpoint(toId, sourceEndpoint, {
            anchor: sourceAnchors,
            uuid: sourceUUID
          });

           var sourceUUID1 = toId+ sourceAnchors1;
          start.addEndpoint(toId, sourceEndpoint1, {
            anchor: sourceAnchors1,
            uuid: sourceUUID1
          });

           var sourceUUID2 = toId + sourceAnchors2;
          start.addEndpoint(toId, sourceEndpoint2, {
            anchor: sourceAnchors2,
            uuid: sourceUUID2
          });
      };
      start.batch(function() {
        start.bind("connection", function(connInfo, originalEvent) {
          init(connInfo.connection);
        });
    
        start.bind("click", function(conn, originalEvent) {
       
        });

        start.bind("connectionDrag", function(connection) {
          console.log(
            "connection " +
            connection.id +
            " is being dragged. suspendedElement is ",
            connection.suspendedElement,
            " of type ",
            connection.suspendedElementType
          );
        });

        start.bind("connectionDragStop", function(connection) {
          console.log("connection " + connection.id + " was dragged");
        });

        start.bind("connectionMoved", function(params) {
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
          addEndpoints(
              id,
              "BottomLeft",
              "BottomCenter",
              "BottomRight"
          );

          
          start.draggable(id, {
              grid: [1, 1],
               //containment: true
          });
        }
      });
      jsPlumb.fire("jsPlumbDemoLoaded", start);
    });
  },
   methods: {
 
    update(){
        
      this.$emit('forceRerender');
      console.log(this.user)
    }
  
  }
}

</script>