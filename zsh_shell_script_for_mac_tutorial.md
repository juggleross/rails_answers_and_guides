0. How to add zsh plugins for ruby?
      
            $ subl ~/.zshrc 
            # add ruby plugins there
            plugins=(rails git ruby)
            
            # ruby - https://github.com/robbyrussell/oh-my-zsh/blob/master/plugins/ruby/ruby.plugin.zsh
            # rails - https://github.com/robbyrussell/oh-my-zsh/blob/master/plugins/rails/rails.plugin.zsh
            # you can add your alias
            alias rb="ruby"

1. How to run sh script?
      
            # install zsh
             zsh (personally I use zsh+oh-my-zsh https://github.com/robbyrussell/oh-my-zsh)
            # create hello.sh script and run it
             zsh hello.sh 
3. How to install zsh?
            
            sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
2. How to puts hello world with script?
            
            echo 'Hello world!'
3. How to create new folder/file?
            
            # folder
            mkdir name
            # file
            touch 1.txt
4. How to open sublime/create a git repo/rub ruby script?
            
            subl new_task.rb
            git init
            ruby new_task.rb
5. How you can open new iterm window?
            
            open . -a iterm
6. How you can declare variables?
            
            a=Hello
            b=world

            echo "$a $b"
            #=> Hello world
            
7. How to exit from code flow?

            echo Hello world
            exit
            echo Does not show
8. How to write conditions?
            
            # -ge == greater than
            # if == end
            age=20

            if [ "$age" -ge 18 ]; then
              echo 'You can vote'
            else
              echo 'You are younger'
            fi
9. You have ability to cancatanate several variabels to one

            prefix=ABC.BCA
            second=1222

            echo $prefix/---$second
            => ABC.BCA/---1222
10. How to write function?
            
            function Welcome() {
              echo "java $1"
            }

            Welcome Hello
11. How to check if string size is zero?
            
            # Checks if the given string operand size is zero
            name=''

            if [ -z $name ]; then
              echo "Is zero!"
            fi
12. How to check if value isn't blank?
            
            name='Tests'

            if [ $name ]; then
              echo "Not zero length!"
            fi
13. How to check if directory exist or not?

            name=test/app/models

            if [ -d $name ]; then
              echo "Is a directory"
            fi
14. Only basename
            
            basename include/stdio.h => stdio.h
15. How to cut field by delimiter?
            
            file_name='saaasad/ssa_1111_222'
            # -d specifies what is the field delimiter that is used in the input file
            # -f specifies which field you want to extract
            $(echo $file_name | cut -d "_" -f 1)
            # => saaasad/ssa
            # you could also extract more than 1 field 
            cut -d "_" -f 1,2,3
            # or range
            cut -d "_" -f 1-3
16. How to cut by sybmols in reverse order?
            
            bic_and_date=FVLBNL20XXX20180412
            $(echo $bic_and_date | rev | cut -c 1-9 | rev)
            #=> 20180412
17. How to use pattern inside shell?

            pat='^(SCT|SDD)_(.+)_(.+)([0-9]{8})\.([0-9]{3})$'
            [[ $file_name =~ $pat ]]
            "${BASH_REMATCH[1]}"
            => SCT
