-  ```
   -> MTT (0.1.0)
    - WARN  | summary: The summary is not meaningful.
    - ERROR | [iOS] unknown: Encountered an unknown error (/usr/bin/xcrun simctl list -j devices

    xcrun: error: unable to find utility "simctl", not a developer tool or in PATH
    ) during validation.
    ```
    [解决办法](https://blog.csdn.net/xjh093/article/details/82888235)

- ```
  - ERROR | [iOS] xcodebuild: Returned an unsuccessful exit code. 
  - NOTE  | [iOS] xcodebuild:  xcodebuild: error: Unable to find a destination matching the provided destination specifier:
    [!] The spec did not pass validation, due to 1 error.
  ```
  [解决办法](https://www.jianshu.com/p/d45d78f4b153)

- ```
    [17:40:44] ~/MTT git(master) ❱❱❱ pod repo push MTSpecs MTT.podspec

    Validating spec
    -> MTT (0.0.2)
        - WARN  | summary: The summary is not meaningful.
        - NOTE  | xcodebuild:  note: Using new build system
        - NOTE  | xcodebuild:  note: Building targets in parallel
        - NOTE  | [iOS] xcodebuild:  note: Planning build
        - NOTE  | [iOS] xcodebuild:  note: Constructing build description
        - NOTE  | [iOS] xcodebuild:  warning: Skipping code signing because the target does not have an Info.plist file and one is not being generated automatically. (in target 'App' from project 'App')
        - NOTE  | [iOS] xcodebuild:  note: Execution policy exception registration failed and was skipped: Error Domain=NSPOSIXErrorDomain Code=1 "Operation not permitted" (in target 'AFNetworking' from project 'Pods')
        - NOTE  | [iOS] xcodebuild:  note: Execution policy exception registration failed and was skipped: Error Domain=NSPOSIXErrorDomain Code=1 "Operation not permitted" (in target 'MTT' from project 'Pods')
        - NOTE  | [iOS] xcodebuild:  note: Execution policy exception registration failed and was skipped: Error Domain=NSPOSIXErrorDomain Code=1 "Operation not permitted" (in target 'Pods-App' from project 'Pods')
        - NOTE  | [iOS] xcodebuild:  note: Execution policy exception registration failed and was skipped: Error Domain=NSPOSIXErrorDomain Code=1 "Operation not permitted" (in target 'App' from project 'App')
        - NOTE  | [iOS] xcodebuild:  warning: MobileCoreServices has been renamed. Use CoreServices instead. (in target 'AFNetworking' from project 'Pods')

    [!] The `MTT.podspec` specification does not validate.
    [17:40:58] [cost 11.400s] 478  pod repo push MTSpecs MTT.podspec
    ```
    解决办法
    ```
    [17:43:10] ~/MTT git(master) ❱❱❱ pod repo push MTSpecs MTT.podspec --allow-warnings
    ```
    
- ```
  Pushing to https://github.com/MTModule/MTHome.git
  To https://github.com/MTModule/MTHome.git
  = [up to date]      0.0.2 -> 0.0.2
  ! [rejected]        master -> master (non-fast-forward)
  error: failed to push some refs to 'https://github.com/MTModule/MTHome.git'
  hint: Updates were rejected because the tip of your current branch is behind
  hint: its remote counterpart. Integrate the remote changes (e.g.
  hint: 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.

  -----------------------------

  [15:51:30] ~/Category_Home git(master) ❱❱❱ git push origin master
  To https://github.com/MTModule/Category_Home.git
  ! [rejected]        master -> master (non-fast-forward)
  error: failed to push some refs to 'https://github.com/MTModule/Category_Home.git'
  hint: Updates were rejected because the tip of your current branch is behind
  hint: its remote counterpart. Integrate the remote changes (e.g.
  hint: 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  [15:51:36] [cost 2.235s] 854  git push origin master
  ```

  其实这个问题是因为 两个 根本不相干的 git 库， 一个是本地库， 一个是远端库， 然后本地要去推送到远端， 远端觉得这个本地库跟自己不相干， 所以告知无法合并
  `git pull origin master --allow-unrelated-histories`
  `git push -f origin master` 强制覆盖
