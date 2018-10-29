<script>
export default {
  name: "VNode",
  functional: true,
  render: (h, context) => {
    return context.props.node;
  }
};
</script>
