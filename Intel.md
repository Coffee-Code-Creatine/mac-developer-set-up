    1  git
    2  xcode-select --install
    3  vi ~/.zshrc
    4  ls
    5  clear
    6  cd Muspelheim
    7  ls
    8  mkdir developer_tools
    9  cd developer_tools
10  ls
11  git clone https://github.com/powerline/fonts.git
12  cd fonts
13  ls
14  ./install.sh
15  ls
16  cd ..
17  ls
18  git clone https://github.com/mbadolato/iTerm2-Color-Schemes.git
19  clear
20  ls
21  mkdir Muspelheim
22  ls
23  echo $PATH
24  history
25  clear
26  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
27  brew
28  brew install zsh
29  sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
30  cd Muspelheim
31  brew install pyenv
32  echo $PYENV_ROOT
33  export PYENV_ROOT=$HOME/.pyenv
34  echo $PYENV_ROOT
35  eval "$(pyenv init -)"
36  vi ~/.zshrc
37  clear
38  cd
39  ls -lap
40  cat .zshrc
41  clear
42  vi .zprofile
43  cat ~/.zprofile
44  source ~/.zprofile
45  brew
46  pyenv install 3.10.4
47  pyenv global 3.10.4
48  python --version
49  clear
50  brew install jenv
51  vi .zprofile
52  source ~/.zprofile
53  jenv enable-plugin export
54  jenv enable-plugin maven
55  python --version
56  brew install java
57  brew install AdoptOpenJDK/openjdk/adoptopenjdk{11,14}
58  brew install AdoptOpenJDK/openjdk/adoptopenjdk8
59  brew install openjdk@17
60  jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/
61  jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home/
62  jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home/
63  jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-14.jdk/Contents/Home/
64  jenv add /usr/local/opt/openjdk@17/libexec/openjdk.jdk/Contents/Home/
65  jenv global 14.0
66  java --version
67  clear
68  vi .zprofile
69  source ~/.zprofile
70  mvn
71  cd
72  brew install nvm
73  mkdir ~/.nvm
74  vi .zprofile
75  source ~/.zprofile
76  ls
77  nvm
78  vi .zprofile
79  source ~/.zprofile
80  nvm
81  clear
82  nvm install node
83  npm install react --save
84  ssh-keygen -t ed25519 -C "coffeecodeandcreatine@gmail.com"
85  pbcopy < ~/.ssh/id_ed25519.pub
86  clear
87  ls
88  cd Muspelheim
89  ls
90  mkdir coffee_code_and_creatine
91  cd coffee_code_and_creatine
92  mkdir repositories
93  cd repositories
94  ls
95  git clone git@github.com:Coffee-Code-Creatine/mac-developer-set-up.git
96  clear
97  ls
98  git clone git@github.com:CoffeeCodeAndCreatine/developer_licenses_and_keys.git
99  cat ~/.zprofile