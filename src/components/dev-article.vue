<template>
    <Layout>
      <Header class="header">
        <Row>
          <i-col span="4" offset="1">
            <img class="logo" src="../assets/logo.png" alt="logo"/>
          </i-col>
          <i-col span="14">
            <Menu mode="horizontal" :active-name="activeName">
              <MenuItem name="/app" to="/app">应用分析</MenuItem>
              <MenuItem name="/push" to="/push">推送营销</MenuItem>
              <MenuItem name="/dev" to="/dev">开发助手</MenuItem>
              <MenuItem name="/manage" to="/manage">应用管理</MenuItem>
            </Menu>
          </i-col>
          <i-col span="4">
            <Row>
              <i-col span="8">
                <Dropdown>
                  <Avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg"></Avatar>
                  <DropdownMenu slot="list">
                    <DropdownItem>我的主页</DropdownItem>
                    <DropdownItem>我的收藏</DropdownItem>
                    <DropdownItem>设置<Badge status="error" /></DropdownItem>
                    <DropdownItem divided="true">退出登录</DropdownItem>
                  </DropdownMenu>
                </Dropdown>
              </i-col>
              <i-col span="8">
                <Dropdown>
                  <Badge :count="count" :offset="[20,4]">
                    <Icon type="ios-notifications" size="24"/>
                  </Badge>
                  <DropdownMenu slot="list">
                    <Tabs value="notification">
                      <TabPane label="通知" name="notification" class="notification">通知的内容</TabPane>
                      <TabPane label="关注" name="follow" class="notification">关注的内容</TabPane>
                      <TabPane label="系统" name="system" class="notification">系统的内容</TabPane>
                    </Tabs>
                  </DropdownMenu>
                </Dropdown>
              </i-col>
              <i-col span="8">
                <Icon type="md-color-palette"  size="24" @click="openTheme = true"/>
              </i-col>
            </Row>
          </i-col>
        </Row>
      </Header>
      <Layout>
        <Sider class="sider" collapsible v-model="isCollapsed">
          <Menu class="sider-menu" theme="dark">
            <MenuItem name="option1">
              <Icon type="ios-search"></Icon>
              <span> 选项一 </span>
            </MenuItem>
            <MenuItem name="option2">
              <Icon type="ios-app"></Icon>
              <span> 选项二 </span>
            </MenuItem>
            <MenuItem name="option3">
              <Icon type="ios-bookmark"></Icon>
              <span> 选项三 </span>
            </MenuItem>
          </Menu>
        </Sider>
        <Content class="content" :class="{ 'content-expand' : isCollapsed }">
            <Breadcrumb class="breadcrumb">
              <BreadcrumbItem to="/">Home</BreadcrumbItem>
              <BreadcrumbItem to="/app">Apps</BreadcrumbItem>
              <BreadcrumbItem>IView</BreadcrumbItem>
            </Breadcrumb>
          <Card style="margin-top: 16px">
            <slot></slot>
          </Card>
        </Content>
      </Layout>
      <Drawer title="选择颜色" v-model="openTheme"></Drawer>
    </Layout>
</template>

<script>
    import ICol from "iview/src/components/grid/col";
    import Breadcrumb from "iview/src/components/breadcrumb/breadcrumb";

    export default {
      components: {
        Breadcrumb,
        ICol},
      name: "devArticle",
      data () {
        return {
          activeName: this.$route.path,
          count: 2,
          openTheme: false,
          isCollapsed: false
        }
      },
      created () {
        this.activeName = this.$route.path
      }
    }
</script>

<style scoped>
  .header {
    width: 100%;
    height: 60px;
    background: #FFF;
    box-shadow: 0px 1px 1px rgba(0,0,0,0.05);
    position: fixed;
    top: 0px;
    left: 0px;
    z-index: 2;
  }
  .logo {
    height: 50px;
    margin-top: 5px;
  }
  .notification {
    text-align: center;
    height: 150px;
  }
  .sider {
    position: fixed;
    height: 100%;
    width: 240px;
    left: 0;
    overflow: auto;
    z-index: 1;
  }

  .sider-menu {
    margin-top: 60px;
  }

  .content {
    margin-top: 60px;
    margin-left: 240px;
    padding: 16px;
    transition: all .2s ease-in-out;
  }

  .content-expand {
    margin-left: 64px;
  }

  .breadcrumb {
    align-content: left;
  }
</style>
