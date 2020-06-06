<template>  
    <div v-on:mouseleave="update"  class="item"  :key="data.label">
        <div id="element1"  class="chart-item" :class="data.shape" :data-key="data.shape">{{data.label}}</div>
    </div>       
</template>
<script>
export default {
    name: 'playsoundaction',
  data() {
    return {
      data: {shape: "rectangle" , label: "Play Sound Action"},
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
      let addEndpoints = function(toId, targetAnchors) {
        console.log(toId, targetAnchors);
          var targetUUID = toId + targetAnchors;
          start.addEndpoint(toId, targetPoint, {
            anchor: targetAnchors,
            uuid: targetUUID
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
            let url = "https://glocum.com";
            let cla = "start";
            let id = "item" + new Date().getTime();
            let html = `<div id="${id}" class="chart-item  ${ui.helper.attr(
              "data-key"
          )}"><div class="${cla}" ><ul><li>Play Sound Action</li></ul></div>${url}<hr></div>`;
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
              "TopCenter"
          );

          
          start.draggable(id, {
              grid: [1, 1]
              // containment: true
          });
        }
      });
      jsPlumb.fire("jsPlumbDemoLoaded", start);
    });
    
  },
   methods: {
 
    update(){
        
      this.$emit('forceRerender3')
    }
  
  }
}

</script>