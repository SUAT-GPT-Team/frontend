SUAT-GPT项目说明文档

SUAT-GPT项目说明文档	1
摘要	1
1. 项目背景	2
2. 项目功能及使用办法	3
3. 项目结构	6
4. 项目开发日志	12
5. 项目未来规划	16
6. 项目遇到的技术难题和解决办法	17
7. 项目成员贡献说明	21
8. 其他信息	22
参考文献	28



摘要
随着人工智能技术的迅猛发展，教育信息化正从传统的“资源数字化”向“智能交互化”转变。 在深圳理工大学积极探索创新教学模式的背景下，如何将静态的教材转化为动态、可交互的智能导师，成为了提升教学质量的关键课题 。
SUAT-GPT 项目正是基于这一现实需求而诞生。 针对《人工智能导论》课程中教材与授课内容脱节、学生预复习效率低等痛点 ，在计算机科学与控制工程学院多位教授的建议与张晓东老师的指导下，本项目团队提出了“书籍变 AI 助手”的创新构想 。作为 Java 程序设计课程的期中实践成果，这不仅是一次代码作业，更是一次完整的软件工程探索 。
在技术实现上， 本系统采用标准的 B/S（浏览器/服务器）架构。后端基于 Spring Boot 框架构建，保障了系统的稳定性与扩展性；前端采用现代化 Web 技术实现交互，并深度集成了通义千问（Qwen）与 DeepSeek 等前沿大语言模型接口 。系统核心功能涵盖 AI 智能交互、学习中心、消息通知中心及个人中心 四大模块，旨在通过“本地知识库 + 生成式 AI”的技术路径，解决教学资源碎片化问题 。
本文档详细记录了 SUAT-GPT 从需求分析、架构设计到部署上线的全过程。 我们希望通过本平台，有效辅助教师备课并提升学生自主学习效率，验证全栈开发技术在校园场景的应用可行性，并为未来构建“深理工 AI 赋能教务生态”奠定坚实的技术与实践基础。
关键词： 智能教学助手；Spring Boot；生成式 AI；校园知识库；前后端分离

1. 项目背景
随着人工智能（Artificial Intelligence，AI）技术在教育领域的快速发展，将传统教材与课程资源转化为可交互的智能学习助手，已逐渐成为教育信息化的重要发展趋势。以弘成 AI 智课、秘塔 AI 等系统为代表的实践表明，通过上传教材或教学资料，即可自动生成结构化课件、课程脚本及辅助讲解内容，从而在一定程度上减轻教师备课负担、提升学生自主学习效率[1]。上述实践为本项目提出的“书籍变 AI 助手”构想提供了直接启发。
与此同时，“内部知识库”建设在高校与企业中日益普及，其核心目标在于整合组织内部的教学、科研与管理资源，构建专属的智能问答与知识检索系统，并通过本地化部署保障数据安全，避免敏感信息外流。例如，山东大学提出了“本地知识库 + 校内版 DeepSeek”解决方案，将办公资料、教学课件和科研文献等统一纳入个人或团队知识库，并借助本地化大模型（如 DeepSeek-R1）实现精准检索与分析，确保“数据不出校”[2]。该模式为高校在教学与科研场景中安全使用生成式 AI 提供了重要参考。
在教学实践层面，2025 年春季学期，深圳理工大学开设的《人工智能导论》课程中，课程指定的参考教材与任课教师实际授课内容及课件之间存在较为明显的脱节现象，部分学生反映难以依托教材进行有效的课前预习与课后复习，进而影响课堂学习效果与整体教学效率。这一问题在一定程度上制约了课程教学目标的达成。
基于上述现实需求、发展愿景以及潜在的教学与科研价值，2025 年 9 月，深圳理工大学教务长赵伟教授在与李金艳教授交流过程中，首次提出“书籍变 AI 助手”的构想，设想开发一个课程知识库平台，将《人工智能导论》教材内容系统性导入，并结合 AI 问答功能，使学生能够围绕教材内容进行提问，服务于预习、复习、备考等完整学习流程，从而同时赋能教师备课与学生自主学习。对此，李金艳教授持审慎态度，指出生成式 AI 容易产生“幻觉”，其输出结果在准确性和可靠性方面仍有待验证，一旦出现错误，可能对教学产生不良影响。他强调，并非否定 AI 在教学中的应用价值，而是需要探索一种更加严谨、可控、可验证的使用方式。
进入 2025 年 11 月，计算机科学与控制工程学院院长潘毅教授亦建议将生成式 AI 技术引入课程辅助与教研支持工作，重点探索其在《人工智能导论》课程中的应用，并安排张晓东老师负责具体推进与落实。在此背景下，本项目团队认为，该系统的研发不仅具备明确的实际应用价值，也能够有效锻炼团队成员的软件工程实践能力，与 Java 课程“完成一个完整程序”的教学目标高度契合。经团队讨论后，决定主动承接该项目，由张晓东老师担任项目指导教师，开展具体的设计与实现工作。
综上所述，本项目定位为“深理工校园知识库”“深理工 AI 赋能教务系统”及“深理工无纸化学习平台”，旨在构建一个面向全校师生的智能学习与知识服务平台，通过对教材与课程资源的系统化整合与智能化处理，提升教学支持能力，探索 AI 技术在高校教学场景中的规范化、可持续应用路径。
2. 项目功能及使用办法
本项目具体分为四大模块及子功能：
- AI入口：提供AI智能交互界面，支持文本对话、课程问答等。用户可直接在此发起对话，系统调用AI模型进行回答。当然，受所调用的AI大模型本身性能影响，个别内容回答会有错误。
 
 
- 学习中心：展示课程列表与内容，包含课程详情、知识点展示、课件资料等。提供课程问答功能，让学生向AI提问课程相关问题（目前未实现）；实现知识点推荐，根据当前学习进度自动推送相关知识与练习（目前未实现）。
   
   
- 消息通知中心：集中推送系统公告、课程通知及作业提醒等。支持教师账号发布通知提醒给指定课程用户，如作业发布、讨论更新等。还集成作业DDL管理，列出所有课程作业及截止日期，以图标或日历形式提醒学生及时完成。
 
- 个人中心：用户个人资料和设置页面。包括账号信息管理（登录/注册、角色切换）、学习统计（学习时长、课程完成度、答题记录等）以及历史消息和聊天记录查询等功能。
   
以上各模块结合实现了一系列核心能力：利用AI进行课程答疑、推荐相关学习资料；通过智能助手功能辅助作业解答（AI作业辅助）；实时发送课程和系统通知；管理学生的作业截止时间；统计学习进度与效果等。
3. 项目结构
3.1 总述
后端系统基于Spring Boot框架搭建。应用启动入口由SuatGptBackendApplication.java提供，配置文件application.yml中设置了服务端口、使用H2内存数据库、JWT密钥和CORS策略等[3]。在WebSecurityConfig中定义了安全过滤链，启用了JWT过滤器，对请求进行拦截验证[3]，以保证后端接口安全。后端采用微服务设计，主要包括认证模块（AuthController 处理登录注册，UserService 加密存储用户信息并在登录后生成JWT）、AI 聊天模块（AiController 接收用户提问并调用AI模型）、数据访问层（使用Spring Data JPA访问用户和聊天记录数据）等[4][5]。
前端采用Vue或React等框架实现单页应用（SPA）形式，与后端通过RESTful API交互。系统采用B/S（浏览器/服务器）架构，前端由Nginx提供静态资源服务，将.js、.css、图片等直接返回给客户端，从而减轻后端负担[6]。研究表明，在静态资源服务方面，Nginx在性能、并发和缓存控制方面优于Spring Boot自带的资源映射，故本项目将前端静态文件交由Nginx托管[6]。后端处理业务逻辑和动态请求，如用户身份验证、AI问答调度等。系统通过JWT（JSON Web Token）方式进行安全认证：用户登录后服务器生成JWT令牌，客户端在后续请求头中带上该令牌，后端验证令牌有效性后才允许访问资源[7][3]。
在AI功能模块方面，系统调用外部大模型接口实现智能对话和知识推理。我们接入了阿里云通义千问（Qwen）系列模型和深度求索（DeepSeek）等先进模型，既包括由科研产业处信息中心提供的只能在校内网络环境调用的API，也包括有本项目成员自费购买的可以在公网调用的API。其中，阿里最新发布的通义千问Qwen 2.5在多项基准测试上性能领先于DeepSeek-V3[8]，保证了AI助手的回答质量和知识覆盖。通过符合OpenAI API标准的接口，后端在AiService中发送用户提问给这些模型，并返回AI生成的响应。所有AI接口调用均需附加经过认证的JWT，确保只有合法用户才能查询模型服务。
3.2 前端结构
SUAT GPT 前端架构思维导图
1.	核心应用与配置 (Core & Config)
•	主入口
o	index.html（挂载点）
o	src/main.tsx（应用启动）
o	src/App.tsx（全局布局与页面组织）
•	构建与工程
o	vite.config.ts、tsconfig.json、package.json（Vite + TypeScript 工程配置）
•	环境与后端地址
o	config/backend.config.ts（后端 API 基址与环境切换）
o	src/utils/api-config.ts（请求基础配置与头信息）
2.	认证模块 (Authentication)
•	页面组件
o	components/AdminLogin.tsx、StudentLogin.tsx（登录入口）
o	components/PersonalCenter.tsx（个人中心）
o	components/AdminDashboard.tsx、pages/admin/（管理员入口与面板）
•	交互流程
o	表单提交 → utils/api.ts 或 utils/api-new.ts → 调用后端 /api/auth/login、/api/auth/register
•	会话与存储
o	utils/storage-fallback.ts（本地存储兜底，用于保存 JWT 等）
3.	AI 聊天模块 (AI Chat)
•	组件
o	components/AIChat.tsx（聊天输入与会话面板）
o	components/AIResponse.tsx（AI 回复展示）
o	components/AISettings.tsx（模型参数与设置）
o	components/CourseAI.tsx（课程上下文内的 AI 辅助）
•	API 封装
o	api/chat.ts（/api/ai/chat、/api/ai/history 的前端封装）
•	数据流
o	用户输入 → api/chat.ts 请求 → 渲染回复与历史消息
4.	课程与学习中心 (Courses & Learning)
•	页面与模块
o	components/CourseDetail.tsx（课程详情）
o	components/CourseFileReader.tsx（课程文件预览/读取）
o	components/HomeworkSection.tsx（作业区）
o	components/LearningCenter.tsx（学习资源聚合）
o	components/TextbookReader.tsx（教材阅读器）
5.	通知与网络诊断 (Notifications & Diagnostics)
•	功能组件
o	components/NotificationCenter.tsx（系统与课程通知）
o	components/NetworkDiagnostics.tsx（API 连通性、权限与 CORS 自检）
•	支撑文档
o	src/403_ERROR_EXPLANATION.txt、403_FIX_SUMMARY.md、FINAL_ERROR_FIX.md 等（403/网络问题排障参考）
6.	UI 组件库 (UI Library)
•	通用组件
o	src/components/ui/*（按钮、表单、对话框、抽屉、下拉菜单、手风琴、图表、走马灯等）
•	设计支持
o	components/figma/ImageWithFallback.tsx（资源占位与容错）
7.	API 与工具层 (API & Utils)
•	请求封装
o	utils/api.ts、utils/api-new.ts（统一请求、错误处理、拦截）
o	utils/console-filter.ts（控制台日志过滤）
•	Supabase 预留
o	utils/supabase/*、supabase/functions/（数据侧扩展与边缘函数）
8.	样式与静态资源 (Styles & Assets)
•	全局样式
o	src/index.css、styles/globals.css
•	静态与构建产物
o	assets/（静态资源）
o	build/index.html、build/assets/*（生产构建输出）
9.	文档与指南 (Docs & Guides)
•	上手与集成
o	docs/QUICK_START.md、JAVA_BACKEND_API.md、API-FLOW-DIAGRAM.md、AI-QUICK-TEST.md
o	src/README*.md、BACKEND_INTEGRATION_GUIDE.md、START_HERE.md、SYSTEM_ARCHITECTURE.md
•	AI 模型与平台
o	docs/AI-MODEL-SWITCH-GUIDE.md、src/AI_MODEL_SWITCH_CHECKLIST.md、AI_MODEL_SWITCH_COMPLETE.md
•	教师/管理员
o	TEACHER_PLATFORM_COMPLETE.md、TEACHER_QUICK_START.md、ADMIN_PLATFORM_GUIDE.md
10.	路由与页面组织 (Routing & Pages)
•	App.tsx 负责页面集成与导航，按角色入口（管理员/学生）组织组件与功能区。

3.3 后端结构
SUAT GPT 后端架构思维导图
1. 核心应用与配置 (Core & Config)
•	主应用
o	SuatGptBackendApplication.java (应用启动入口)
•	配置
o	application.yml (端口: 8080, DB: H2 内存, JWT 密钥, CORS 策略)
o	config/WebSecurityConfig.java (定义安全链、启用 JWT 过滤器、配置 CORS)
o	config/JwtTokenFilter.java (拦截请求，解析并验证 JWT Token)
2. 认证模块 (Authentication)
•	控制器
o	controller/AuthController.java (路由: /api/auth/register, /api/auth/login)
•	服务
o	service/UserService.java (核心业务逻辑)
	注册 (registerUser): 检查用户名唯一性，密码加密，保存。
	登录 (loginAndGenerateToken): 委托 AuthenticationManager 认证，成功后生成 JWT。
o	service/SecurityUserDetailsService.java (安全集成)
	loadUserByUsername: 从 DB 加载 User，转换为 Spring Security 的 UserDetails。
•	工具
o	utils/JwtUtils.java (JWT Token 处理器)
	生成 Token (Subject=Username, Claims, Expiration)
	验证 Token (isTokenValid)
	提取用户名 (extractUsername)
3. AI 聊天模块 (AI Chat)
•	控制器
o	controller/AiController.java (路由: /api/ai/chat, /api/ai/history)
	/chat: 接收用户消息，调用 AiService，返回 AI 响应。
	/history: 获取用户历史消息列表。
•	服务
o	service/AiService.java (AI 业务逻辑)
	processUserMessage: 调用 AI 模型，存储用户和 AI 的两条 ChatMessage 记录。
	getChatHistory: 从 ChatMessageRepository 获取历史记录。
4. 数据层 (Model & Repository)
•	实体 (Model)
o	model/User.java (主实体)
	字段: id, username, password, role
	关系: 1 : N (拥有多条 ChatMessage)
o	model/ChatMessage.java (从属实体)
	字段: id, user_id (外键), sender, content, timestamp
	关系: N : 1 (属于一个 User)
•	数据访问 (Repository)
o	repository/UserRepository.java
	findByUsername, existsByUsername
o	repository/ChatMessageRepository.java
	findByUserOrderByTimestampAsc (按时间获取用户的聊天历史)


4. 项目开发日志
•	2025.11.12：
o	项目组在八分饱餐厅召开第一次会议，确定项目概念、项目目标、大致分工安排。
•	2025.11.19：
o	完成前端整体架构设计；
o	绘制并确认功能模块架构图；
o	设计出演示界面；
o	借助PowerPoint和用于设计前端的AI软件（Figma）实现初步界面的代码生成；
o	购买Figma会员账号；
o	通过查找资料，对前后端技术栈和调用关系进行学习和梳理。
  
 
•	2025.11.21：
o	张晓东老师向信息中心申请了AI模型接口。有时间限制，到12月21日为止。
o	创建在线共享文档《工作总结》，建立工作日志制度。
•	2025.11.27：
o	提出技术选型、后端架构方案。
•	2025.11.28：
o	实现在前端接入AI模型接口；
o	完成通义千问和DeepSeek的API调用示例；
o	在前端增加了滚轮功能；
o	搭建后端基础环境，包括初始化Spring Boot项目、配置Supabase后端数据库并完成初步连接。
•	2025.11.30：
o	完成前端全部核心功能设计；
o	通过查找资料学会了后端和服务器的关系。
•	2025.12.01：
o	完成后端基本代码和架构。
•	2025.12.02：
o	前后端接口联调成功，实现用户登录、聊天和消息通知的基本功能；
o	发现开发环境的防火墙阻碍了模型API访问，并及时解决该网络问题。
o	完成了初始Demo，能在本地运行。
•	2025.12.03：
o	成功实现把模型部署到Demo网站：suat.ms1001.com上；
o	深入理解并掌握了前后端分离架构下的独立构建与打包流程。
•	2025.12.04：
o	成功把AI集成到后端，建立前后端接口。
o	项目组在19栋4楼召开第二次会议，明确先第一步跑起来，再优化细节和扩展功能，明确后续任务分工：
	1. 开展RAG（检索增强生成）技术调研——李之城，胡子豪
	2. 写软件说明和操作指南——李之城，叶顾霖
	3. 由“效率部”对前端UI进行简化改版以提升性能，删除无用的内容——任可滢，叶顾霖
	4. 解决长问题无法回复报错的问题——梁进杰
	5. 后端增加响应速度优化，解决时间（响应慢）问题——任可滢，叶顾霖
	6. 交作业与服务器部署——李之城，梁进杰
	7. 探索使用Docker对服务进行容器化部署——李之城
	8. 创建并维护GitHub项目仓库便于协作——李之城
•	2025.12.05：
o	创建项目的GitHub地址：https://github.com/SUAT-GPT-Team；
o	学会如何使用GitHub进行项目协作；
o	明确我们的系统一定属于 B/S（Browser–Server）架构而不是cs（即client-server）架构。
•	2025.12.08：
o	和开发其他APP的成员进行交流，了解他们打包apk的主要方式和痛点，了解他们项目的特色。
o	对Weknora 、Coze、Dify、RAGFlow与n8n等知识库进行调研。
o	代码重构与轻量化：对前端项目进行了深度清理，移除冗余文件与依赖，优化项目体积与运行效率（实现前端“大裁员”）。
o	完成PWA（渐进式Web应用）封装打包，支持安装APP形式使用；对教师和学生两类账号登录进行了功能测试，完善了权限控制。
•	2025.12.11：
o	在程嘉锐的指导下，把后端调用API的代码首次成功部署到服务器上；并成功运行验证；
o	参照张晓东老师建议，准备了校内服务器部署方案。
o	优化输出排版，实现流式输出，能够折叠思考过程。
•	2025.12.12：
o	项目组在19栋4楼召开第三次会议，明确后续任务分工：
	1. 本周建立《人工智能导论》课程到数据库，同步到前端，包括：课程名称、教师、上课时间、课件（文件如何上传）
	2. 本周建立教师测试账号、学生测试账号，教师账号具备上传课件、新增通知的权限，学生账号只能查看。
	3. 本周添加一些通知。
	4. 本周封装打包。
	5. 寒假，重点研究RAG问题，可以考虑RAGFlow、腾讯Wekrona、AnythingRAG。
o	实现了学习中心、通知中心和个人中心框架。
o	实现了学生端和教师端登陆功能。
•	2025.12.14：
o	对项目进行打包成.apk文件。
•	2025.12.15：
o	完成项目说明文档写作，提交Java作业。
5. 项目未来规划
•	5.1 学期内目标
o	实现课程课件上传与管理功能；
o	完善通知发布与推送机制；
o	建立课程基础数据库，填充典型教学资源；
o	配置测试账号并完成发布上线流程，为学期教学做好准备。
•	5.2 寒假目标：
o	深入研究RAG技术，尝试将课程文档和课件做嵌入式知识检索，打通检索增强生成流程[9]。计划使用 LangChain 或 RAGFlow 框架，结合向量数据库（如 Milvus 或 PostgreSQL pgvector）实现本地知识库的切片与检索。
o	计划开发文档上传与向量化检索功能，使AI助手能够基于文档内容提供更精确的问答辅助。
•	5.3 长期目标：
o	逐步建设完整的SUAT AI生态系统，涵盖智能教学辅助、科研助手等多种应用场景。
o	探索发表软著、申请相关技术专利，将项目部署到校内服务器集群上；
o	后续规划新增教学评估分析、科研数据分析辅助等功能，使平台成为校内教育与科研的综合智能平台。
o	安全加固：修复CORS跨域配置，将 * 通配符收紧为指定的域名白名单，防止CSRF攻击。

6. 项目遇到的技术难题和解决办法
•	6.1 涉及前端页面相关
o	6.1.1 页面无法滚动问题：在前端聊天界面中发现，当AI回答较长时，无法向下滚动，导致只能通过缩放页面来查看，导致信息不全。对此，我们通过优化前端代码增加了滚动功能。
o	6.1.2 AI思考结果无法折叠问题：传统的AI模型问答界面中，一般都折叠思考过程，方便用户分清楚思考过程和正式回答内容。而通过大模型API调用的AI思考结果不会自动折叠，对此，我们修改前后端代码，为调整聊天组件逻辑，优化答题卡片的CSS样式，使回答内容可完整展开。
o	6.1.3 响应速度慢： AI问答响应初期速度较慢。经研究，主要是因为没有实现流式输出，都是全部输出完才一次性体现，对此，通过修改前后端代码，实现了流式输出，解决了这个问题。引入流式输出（Streaming）后，首字响应时间（TTFB）从平均3秒降低至0.5秒以内，显著提升了用户体验。
•	6.2 涉及服务器部署相关
o	6.2.1 向科研产业处信息中心申请使用的大模型服务部署在学校本地服务器，仅能通过学校内网访问，调用时需填写校内 IP 地址。而本项目最初部署在成员的个人云服务器上，属于公网服务器，无法访问学校内网资源，导致该大模型接口在实际运行中无法使用。解决方案是在系统架构设计上，将 SUAT-GPT 拆分为“在线版”与“本地版”两种形态。在线版部署在公网服务器，仅保留基础对话能力，使用公网可访问的大模型接口（如公网千问），无法调用校内内网部署的大模型及部分校内服务，属于功能阉割版；本地版：部署在用户本地环境，可完整调用校内内网大模型及相关服务，属于功能完整版。两种版本在功能、模型来源及部署环境上的具体差异详见8.4、8.5 节。未来计划联系学院、信息中心或党宣部门，争取在校内服务器上正式部署本项目，从而统一为完整版本运行。
o	6.2.2 在本地部署中，前端发出的url请求通过localhost访问到本地服务器，但如果部署到服务器时，会出现前端的url请求无法通过localhost到达服务器，因为前端是运行在电脑而电脑localhost没有springboot，有两个解决方案。
	（1）将前端服务器url改为服务器ip，并且在服务器的权限认证中对所有公网ip开放（原模式为只对localhost开放）。
	（2）使用nginx反向代理，将前端的api/**请求映射到服务器本地的localhost:8080，这样可以直接访问springboot
	观察到宝塔的nginx主配置中已经存在方法（2），我们便基于此修改，但出现一个问题，除了主配置文件还有/www/server/panel/vhost/nginx/suat.ms1001.com.conf这个文件也在监听80端口做映射，但服务器只允许一个监听，导致写在主配置的映射被忽视，所以将映射加入这个conf即可。
o	6.2.3 还存在一个问题，前两个改动在allowed-origins改为"*"后（对所有ip皆可访问）可正常使用公网千问（qwen-public），但在改回localhost:3000后会报403，原因疑似是token在浏览器的认证问题，这点未解决。改为"*"是一个临时解决办法，但会存在api泄露。
•	6.3 涉及项目总体架构相关
o	6.3.1 在开发前端时，因为本项目成员没有学过前端语言，不具备开发前端的基础，我们选择了购买Figma会员，通过在PowerPoint上制作的一张设计图让Figma生成相应的前端内容，效果还不错。
o	6.3.2 我们选择通过先制作网页，再打包成apk的方式来完成项目，而非直接通过Android Studio来做，主要是考虑到网页作为一种可以在各种设备打开的载体，这样覆盖面更广，同时有一个固定域名也有利于项目推广。在从网页打包封装为.apk的过程中，经查询，有三种方式，一种是WebView 封装成 APK（最快 / 不用上架）；另一种是PWA（Progressive Web App）——不用上架，也不用封装 APK；第三种是从头写，用Android  Studio开发真正的原生 App，但是可以模仿前端的逻辑，只用写前端，后端可以共用。从效率的角度出发，我们选择第三方软件帮我们直接打包。
o	6.3.3 关于系统架构，目前一般的系统架构分两种，一种是cs，即client-server。client是客户端，比如一个简单APP，只是提供一个交互界面，与服务端server做数据的交互；再一种是bs，即browser-server。浏览器是前端，所有的代码都是在server端。比如server有个index.html，是系统的入口。浏览器打开的一般就是这个。我们的系统一定属于 B/S（Browser–Server）架构，“客户端”就是浏览器，前端看似复杂，但打包以后只有index.html，JS，CSS三个文件；这些文件都是通过 Nginx（宝塔）从服务器上提供的静态资源，浏览器只负责显示界面，不处理业务逻辑。至于前端打包前有几万个文件的情况，后续我们进行了处理；所有真实逻辑都在 Server（后端），后端 Spring Boot 程序负责：用户输入流转到模型，调用 LLM，历史记录、RAG 逻辑，API 安全校验，各种业务控制。浏览器只负责发出请求。前端不是“客户端”，它只是静态页面。我们要把功能模块解耦，每个模块功能尽量单一，各司其职就好。
•	6.4 涉及前后端连接相关
o	6.4.1 前后端接口调试失败：在本地联调阶段，多次出现前端、后端代码本身都正常，但前端无法正常调用后端接口，出现403、502等故障的问题。后来借助GitHub Copilot的代码分析功能，自动识别并修复了前后端接口的潜在冲突。推测问题可能与CORS跨域配置或请求头格式有关，经自动化工具调整后恢复正常。当然，经过长期的经验总结，我们也发现两点：
	运行这个项目的时候，在命名项目的文件夹名称里面尽量不要有中文，要保证全英。
	我们经常在其他校区编辑软件，如果出现“对不起，AI服务 (qwen-internal) 调用失败，请检查网络（公网/内网）或 API Key。”的提示，则说明服务是正常的，只是因为我们不在主校区，所以连不上。
o	6.4.2 Supabase数据库权限配置：一开始我们打算用Figma软件自带的Supabase功能，直接用AI生成后端代码再稍作修改，后来发现Supabase无法生成Java代码，所以弃用此方案。
•	6.5 其他技术问题
在项目过程中，除上述提到的主要问题外，我们还出现了一系列技术问题，但都通过咨询大模型顺利解决，因为对最终效果影响不大，在此不再赘述每一个问题的解决过程，仅大致列出核心问题供参考和回顾。
o	安全、跨域与 Spring Security 相关问题：WebSecurityConfig 在哪里？为什么改完安全配置就各种 does not exist？Spring Security 相关包全部找不到？403 Forbidden 是怎么来的？allowed-origins 改成 "*" 就好了，改回就不行，为什么？通过咨询大模型，我们认识到，一大段报错，实际上集中反映了：Maven 依赖未正确引入 / 版本不匹配；Spring Boot 2 vs 3（javax.servlet vs jakarta.servlet）；Spring Security 新旧写法差异；浏览器跨域 + Token 鉴权的组合问题。这是后端安全配置 + Web 安全模型的综合问题。
o	Nginx、宝塔与服务器配置问题：如何查找 nginx 配置文件？宝塔中为什么配置了但不生效？主配置 vs vhost 配置有什么区别？为什么监听 80 端口会冲突？为什么写在 nginx.conf 里的规则没生效？最终我们认识到，宝塔会为每个域名单独生成/www/server/panel/vhost/nginx/xxx.conf，实际生效的是这里，而不是主配置。这是真实服务器运维级别的问题。
o	后端启动、运行与部署相关问题（Spring Boot / Java）：后端启动命令是什么？后端启动的代码是什么？如何在宝塔服务器中输入命令打开后端 Java？现在宝塔搞不了，请分析原因？改了安全配置之后，本地还能不能运行？还是只能云端？通过咨询大模型，我们认识到，这些问题集中反映出三个核心困惑：Spring Boot 启动方式（IDE / 命令行 / jar）；本地环境 vs 云端环境的差异；宝塔只是“面板”，真正跑的是 Linux + Java + Nginx。
o	Web 基础认知问题：前端三部曲是啥？403 / 404 错误是什么意思，有什么区别？广域网 / 城域网 / 局域网是什么？浏览器访问一个网站，本质发生了什么？
o	关于GitHub的问题：New repository / organization / project / codespace 有什么区别？我们项目应该用哪个最合适？个人项目如何转移到团队 organization？能不能一次性上传整个文件夹？GitHub 客户端能不能做到？如何安装 Git？Git LFS 是什么？如何 migrate？Codespace 为什么不能用？能不能直接部署成网站？GitHub Pages 是什么？效率高不高？适不适合做可随时更新的个人网页？
o	大模型与 AI 技术选型问题：开源的 RAG 大模型有哪些？谷歌 Gemini 是不是用的 BERT？校内部署的大模型为什么只能内网访问？公网模型 vs 校内模型如何共存？
7. 项目成员贡献说明
根据项目分工和任务记录，各成员贡献如下：
- 李之城：负责系统整体架构设计，负责前端开发和Figma设计实现；负责把项目部署到服务器及PWA封装；协管集成AI模块（Qwen、DeepSeek）接口；负责项目版本管理和团队协作（GitHub仓库管理）等。
- 任可滢：协管系统整体架构设计；负责后端服务开发与维护，编写Spring Boot控制器和业务逻辑；负责调试前后端接口，完善JWT认证流程和权限策略；负责系统功能测试与性能优化，删除无用的内容。
- 梁进杰：负责前后端功能升级，包括滚动功能、教师/学生登录功能、学习中心、通知中心、个人中心开发等；优化后端响应逻辑和前端渲染效率，提升整体性能；协管把项目部署到服务器及PWA封装。
还有三位同学虽然不是本“Java期中作业”团队的正式参与者，但也对本项目提供了支持、做出了贡献，特说明如下：
- 叶顾霖：负责优化前端界面与交互实现，优化用户体验。
- 胡子豪：负责调研RAG的开发模式。
- 程嘉锐：通过配置Nginx反向代理和服务器环境等方式，解决了项目部署到服务器过程中出现的问题。
8. 其他信息
•	8.1 项目的备份和存储
o	GitHub仓库地址：项目源码已托管在GitHub，项目地址为：https://github.com/SUAT-GPT-Team/，欢迎团队成员协作开发。
o	前端项目在Figma生成的基础上做了修改，原项目可参考：https://www.figma.com/design/w0tuZHZm6rC03LGJL69Cp4/suatgpt-frontend/。
•	8.2 接口Key
o	已成功申请到阿里云通义千问和深度求索的API密钥并记录在项目文档中。
o	其中“内网”AI服务受信息中心影响，可能偶尔不可用。
•	8.3 测试账号
o	学生账号：zhangsan
o	密码：123456
o	教师账号：admin
o	密码：admin123
o	教师账号：teacher
o	密码：teacher123
•	8.4 本地版和在线版的区别
o	在线版暂时没有使用校内Qwen3-30B (内网)、DeepSeek-R1的能力。
o	在线版暂时没有使用学习中心、通知中心、个人中心的能力。
o	在线版可以在https://suat.ms1001.com/访问，也可以通过我们提供的apk访问。

•	8.5 本地版开发环境配置

8.5.1 运行逻辑
SUAT-GPT 本地版采用前后端分离架构，运行时需要先启动 Spring Boot 后端服务（8080 端口），再启动前端开发服务器（Vite / Vue / React）（3000 端口），前端通过 /api/** 接口与后端交互。

8.5.2 项目目录结构说明（示例）
假设项目统一放在如下目录中：
D:\SUATGPT-V4\
│
├─ backend\          ← 后端（Spring Boot + Maven）
│   ├─ pom.xml
│   ├─ src\
│   └─ target\
│
└─ frontend\         ← 前端（Vite）
    ├─ package.json
    ├─ vite.config.ts
    └─ src\
后续所有命令，都在对应目录下执行。

8.5.3 运行后端（Spring Boot，本地版）
8.5.3.1 后端运行前的准备（一次性）
1️⃣ 安装 JDK（必须）
•	推荐版本：JDK 17
•	安装完成后，在 CMD 中验证：
java -version
看到 java version "17.x" 即说明成功。

2️⃣ 安装 Maven 并配置环境变量（必须）
1.	Maven 官网下载
👉 https://maven.apache.org/download.cgi
下载 Binary zip archive
2.	解压到任意目录，例如：
D:\apache-maven-3.9.9\
3.	配置环境变量（具体参照https://blog.csdn.net/2301_76357803/article/details/136013359?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522c97a3a7e6995b716fed99d19849e5895%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=c97a3a7e6995b716fed99d19849e5895&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-136013359-null-null.142^v102^control&utm_term=Maven%E4%B8%8B%E8%BD%BD&spm=1018.2226.3001.4187，大致流程如下）
•	新增系统变量：
o	变量名：MAVEN_HOME
o	变量值：D:\apache-maven-3.9.9
•	在 Path 中新增：
•	%MAVEN_HOME%\bin
4.	CMD 中验证：
mvn -v
能看到 Maven 版本信息即可。

8.5.3.2 运行后端

方式一：使用 CMD 直接运行后端（最稳定，推荐）
1️⃣ 打开 CMD，进入后端目录
cd D:\SUATGPT-V4\backend

2️⃣ 下载依赖并编译项目
mvn clean package -DskipTests
第一次运行会比较慢（下载依赖），属于正常现象。

3️⃣ 启动 Spring Boot 后端
方式 A：直接用 Maven 启动（调试友好）
mvn spring-boot:run
方式 B：运行打包好的 jar（更接近真实部署）
java -jar target\suat-gpt-backend-0.0.1-SNAPSHOT.jar

4️⃣ 判断后端是否启动成功
在控制台看到类似内容：
Tomcat started on port(s): 8080
Started SuatGptBackendApplication in xx seconds
说明后端已经成功运行，监听端口为 8080。
你也可以在浏览器中测试：
http://localhost:8080/api/health

方式二：使用 VS Code 运行后端（开发用）
1️⃣ VS Code 必装插件（4 个）
在 VS Code 扩展商店中安装：
•	Extension Pack for Java
•	Spring Boot Extension Pack
•	Language Support for Java
•	Debugger for Java

2️⃣ 在 VS Code 中配置 Maven
•	打开 VS Code → 设置
•	搜索 maven
•	确认 Maven 路径已正确识别
（可参考你给的教程链接）

3️⃣ 打开后端目录
File → Open Folder → D:\SUATGPT-V4\backend

4️⃣ 运行后端
方式一（推荐）：
•	打开主启动类
SuatGptBackendApplication.java
•	点击 Run / Debug
方式二：
•	打开 VS Code 终端，执行：
mvn spring-boot:run

8.5.4 运行前端（Vite 项目）
⚠️ 注意：后端必须已经启动，前端才能正常请求接口

8.5.4.1前端运行前的准备
1️⃣ 安装 Node.js（LTS）
•	官网：https://nodejs.org
•	安装完成后验证：
node -v
npm -v

2️⃣ Windows 脚本权限问题（如出现 npm 报错）
如果出现：
running scripts is disabled on this system
请 以管理员身份 打开 PowerShell，执行：
Set-ExecutionPolicy RemoteSigned
输入 Y 确认。

8.5.4.2 启动前端
1️⃣ 打开 CMD，进入前端目录
cd D:\SUATGPT-V4\frontend

2️⃣ 安装依赖（只需第一次）
npm install

3️⃣ 启动前端开发服务器
npm run dev

4️⃣ 判断前端是否启动成功
控制台看到类似内容：
Local:   http://localhost:3000/
在浏览器打开：
http://localhost:3000
即可访问 SUAT-GPT 本地版前端界面。

8.5.5 本地版整体运行顺序总结
正确顺序只有一个：
① 启动后端（8080）
② 再启动前端（3000）
③ 浏览器访问前端地址
对应端口关系：
模块	地址
后端	http://localhost:8080

前端	http://localhost:3000

前端 → 后端	/api/**

8.5.6 常见问题（小白最容易卡的地方）
❓ 前端报错 ECONNREFUSED
原因：后端没启动 / 端口不对
解决：
•	确认后端正在运行
•	确认后端端口是 8080

❓ 浏览器返回 403
原因：Spring Security / CORS 配置问题
解决：
•	本地版 allowed-origins 建议先使用：
•	http://localhost:3000


•	8.6 参考文献：
o	在项目结构部分，我们参考了Spring Boot与Nginx静态资源服务的相关经验[6]；
o	在安全认证方面采用了Spring Security+JWT方案[7]；
o	在AI模型选择方面参考了阿里通义千问与DeepSeek的性能比较[8]；
o	规划RAG技术时参考了检索增强生成（RAG）的原理说明[9]；
o	校园知识库理念参考了山东大学深度求索本地化方案[2]；
o	教材数字化案例参考了弘成AI智课的模式[1]。
o	这些资料为本项目设计提供了重要借鉴。

•	8.7 致谢
o	我们感谢赵伟教务长、潘毅院长、李金艳教授对本项目思路的启发，感谢张晓东老师的具体指导，感谢周桥桥老师、马智恒老师为本项目提供具体的应用场景和机会，感谢参与项目及为项目提供帮助的所有同学（李之城、任可滢、梁进杰、叶顾霖、胡子豪、程嘉锐等）为本项目做出的努力。

参考文献
[1] 弘成AI智课： “三步”让一本书“活”起来
https://www.chinaedu.net/html/news/20250911141331.html
[2] 本地知识库+校内版DeepSeek-R1使用手册-山东大学信息化工作办公室
https://www.nc.sdu.edu.cn/info/1171/2220.htm
[3] [4] [5] 070e3ce9-83c7-4d74-8cff-e8a33595a93b.docx
file://file_00000000da287209b1bed73a30cb10c9
[6] 用 Spring Boot 静态资源映射 vs 用 Nginx 提供静态文件服务总结_springboot 静态资源鉴权nginx-CSDN博客
https://blog.csdn.net/J080624/article/details/148350962
[7] Springboot集成Spring Security实现JWT认证 - 南瓜慢说 - 博客园
https://www.cnblogs.com/larrydpk/p/14939748.html
[8] 阿里巴巴发布AI模型 声称超越DeepSeek
https://www.voachinese.com/a/alibaba-releases-ai-model-it-claims-surpasses-deepseek-v3-20250129/7955186.html
[9] RAG技术详解：融合检索与生成的AI大模型 - 小灰灰的笔记
https://www.tinyash.com/blog/rag/
