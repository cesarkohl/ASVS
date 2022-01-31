# 评估和认证

## OWASP对ASVS认证和信任标志的立场

OWASP作为一个与供应商无关的非营利性组织，目前不认证任何供应商、验证人员或软件。

所有这类保证声明、信任标志或认证，均未经 OWASP 正式审查、注册或认证，因此依赖此类观点的组织，需要谨慎对待任何第三方的信任或声称ASVS认证的信任标志。

这并不影响组织提供此类保证服务，只要他们不要求官方的 OWASP 认证。

## 认证组织指南

应用程序安全验证标准，可以用作应用程序的公开验证，包括对关键资源的开放和自由访问（如架构师和开发人员、项目文档、源代码），对测试系统的认证访问（包括对每个角色的一个或多个帐户的访问），特别是L2和L3验证。

从历史上看，渗透测试和安全代码审查都包含“异常”问题——即只有未通过的测试项才会出现在最终报告中。 认证组织必须在任何报告中包括验证的范围（特别是某个关键组件不在范围内时，如SSO身份验证）、验证结果的摘要，包括通过的和未通过的测试，并清楚地说明如何解决未通过的测试。

某些验证要求可能不适用于被测试的应用程序。例如，如果你向客户提供无状态的服务层API而没有客户端实现，那么“V3-会话管理”中的许多要求就不能直接使用。 在这种情况下，认证机构仍可声称完全符合 ASVS 的要求，但必须在报告中明确说明被排除的验证要求不适用的原因。

保留详细的工作底稿、屏幕截图或视频、可靠地重复利用一个问题的脚本，以及测试的电子记录，如拦截代理日志和相关的笔记（如清理清单），被认为是标准的行业惯例，哪怕是对于最可疑的开发人员来说，它们也能作为调查结果的证明。 仅仅跑一个工具并报告故障是不够的，这根本不能提供充分的证据，证明所有认证级别的问题都经过了彻底的测试。 在有争议的情况下，应该有足够的证据，来证明每一个经过验证的需求确实被测试过。

### 测试方法

认证机构可自由选择适当的测试方法，但应在报告中注明。

根据所测试的应用程序和验证需求，可以使用不同的测试方法来获得相似的结果置信度。 例如，要验证应用程序输入验证机制的有效性，可以通过手动渗透测试或通过源代码来分析。

#### 自动化安全测试工具的作用

鼓励使用自动化渗透测试工具以提供尽可能多的覆盖范围。

仅使用自动渗透测试工具，是不可能完全完成ASVS验证的。虽然L1中的绝大多数需求可以使用自动化测试来执行，但总体上，绝大多数需求并不适合自动化渗透测试。

请注意，随着应用安全行业的成熟，自动化和手动测试之间的界限已经变得模糊。 自动化工具通常由专家手动调整，而手动测试人员通常会利用各种自动化工具。

#### 渗透测试的作用

在 4.0 版本中，我们决定让 L1 完全可渗透测试，而无需访问源代码、文档或开发人员。 OWASP Top 10 2017 A10 要求的两个日志记录项目，将需要访谈、屏幕截图或其他证据，就像它们在 OWASP Top 10 2017 中的一样。 然而，在无法获得必要信息的情况下进行测试，并不是一种理想的安全验证方式，因为它不仅错过了审查来源、识别威胁和缺失控制的可能性，还会错过在更短的时间内进行更彻底测试的可能。

在可能的情况下，执行L2或L3评估时，需要访问开发人员、文档、代码，以及访问具有非生产数据的测试应用程序。 在这些级别进行的渗透测试，需要这种级别的访问，我们称之为 “混合审查” 或 “混合渗透测试”。

## ASVS的其他用途

除了用于评估应用程序的安全性外，我们还确定了ASVS的许多其他潜在用途。

### 作为详细的安全架构指南

应用程序安全验证标准的更常见用途之一，是作为安全架构师的资源。 Sherwood应用业务安全架（Sherwood Applied Business Security Architecture，SABSA）缺少大量的信息，而这些信息是完成一次彻底的应用安全架构审查所必需的。 ASVS可以用来填补这些空白，让安全架构师为常见问题选择更好的控制措施，如数据保护模式和输入验证策略。

### 作为现有安全编码Checklists的替代品

许多组织可以从采用ASVS中受益，通过选择三个级别中的一个，或通过fork ASVS，在特定领域改变每个应用风险级别的要求。 我们鼓励这种fork，只要保持可追溯性，因此，如果一个应用程序已经通过了标准版本中的“要求4.1”，那么也就通过了fork版本中的这个要求。

### 作为自动化单元和集成测试的指南

ASVS的设计是高度可测试的，唯一的例外是架构和恶意代码要求。 通过构建单元和集成测试，对相关的滥用情况进行fuzz测试，应用程序几乎可以在每次构建中进行自我验证。 例如，可以为登录控制器制作额外的测试，测试常见的默认用户名参数、帐户枚举、暴力破解、LDAP注入、SQL 注入以及 XSS。 同样地，对密码参数的测试，应该包括常用密码、密码长度、空字节注入、移除参数、XSS等。

### 用于安全开发培训

ASVS 还可用于定义安全软件的特征。 许多“安全编码”课程只是带有少量编码技巧的道德黑客课程。 这不一定能帮助开发人员编写更安全的代码。 相反，安全开发课程可以使用 ASVS，重点关注 ASVS 中的主动控制，而不是前 10 项不该做的负面事情。

### 作为敏捷应用安全的驱动程序

在敏捷开发过程中，为了获得安全的产品，ASVS可以作为框架来定义团队需要实施的特定任务。 一种可能的方法是：从 Level 1 开始，根据指定级别的 ASVS 要求，验证特定应用程序或系统，查找缺少哪些项目，并在待办事项中提出特定工单/任务。 这有助于对具体任务进行优先排序（梳理），并使安全在敏捷开发中可见。 这也可用于确定组织中审计和审查任务的优先；其中，特定的 ASVS 要求，可以作为团队成员审查、重构或审计的驱动因素，并可以记录到最终的待办清单中。

### 作为指导安全软件采购的框架

ASVS 是一个很好的框架，可以帮助确保安全软件的采购或定制开发服务的采购。 买方可以简单地设定一个要求，即他们希望采购的软件必须按照 ASVS 的 Level x 来开发，并要求卖方证明该软件满足ASVS的x级。