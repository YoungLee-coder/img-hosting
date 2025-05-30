graph TB
    %% 用户角色
    User((用户))
    Guest((访客))
    
    %% 系统边界
    subgraph GoodSticks["GoodSticks 备忘录系统"]
        %% 认证相关用例
        subgraph AuthModule["用户认证模块"]
            UC1[用户注册]
            UC2[用户登录]
            UC3[记住密码]
            UC4[用户注销]
        end
        
        %% 笔记管理相关用例
        subgraph NoteModule["笔记管理模块"]
            UC5[创建笔记]
            UC6[编辑笔记]
            UC7[删除笔记]
            UC8[查看笔记列表]
            UC9[搜索笔记]
            UC10[置顶笔记]
            UC11[添加图片]
            UC12[拍照添加]
            UC13[从相册选择]
        end
        
        %% 个性化设置相关用例
        subgraph SettingsModule["个性化设置模块"]
            UC14[切换主题色]
            UC15[切换深色模式]
            UC16[查看应用信息]
        end
        
        %% 数据同步相关用例
        subgraph SyncModule["数据同步模块"]
            UC17[备份数据]
            UC18[恢复数据]
            UC19[WebDAV配置]
        end
        
        %% 启动相关用例
        subgraph StartupModule["应用启动模块"]
            UC20[应用启动]
            UC21[检查登录状态]
        end
    end
    
    %% 外部系统
    Camera[相机系统]
    Gallery[图库系统]
    WebDAVServer[WebDAV服务器]
    FileSystem[文件系统]
    
    %% 用户与用例的关系
    User --> UC2
    User --> UC4
    User --> UC5
    User --> UC6
    User --> UC7
    User --> UC8
    User --> UC9
    User --> UC10
    User --> UC11
    User --> UC14
    User --> UC15
    User --> UC16
    User --> UC17
    User --> UC18
    User --> UC19
    
    Guest --> UC1
    Guest --> UC20
    Guest --> UC21
    
    %% 用例之间的关系
    UC2 -.->|<<include>>| UC3
    UC20 -.->|<<include>>| UC21
    UC11 -.->|<<extend>>| UC12
    UC11 -.->|<<extend>>| UC13
    UC5 -.->|<<include>>| UC11
    UC6 -.->|<<include>>| UC11
    
    %% 系统依赖关系
    UC12 --> Camera
    UC13 --> Gallery
    UC17 --> WebDAVServer
    UC18 --> WebDAVServer
    UC11 --> FileSystem
    
    %% 样式定义
    classDef userStyle fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef systemStyle fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef moduleStyle fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef externalStyle fill:#fff3e0,stroke:#e65100,stroke-width:2px
    
    class User,Guest userStyle
    class GoodSticks systemStyle
    class AuthModule,NoteModule,SettingsModule,SyncModule,StartupModule moduleStyle
    class Camera,Gallery,WebDAVServer,FileSystem externalStyle
