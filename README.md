# devops-netology
Sarkisyan Aleksey


#1. хеш коммита aefead2207ef7e2aa5dc81a34aedf0cad4c32545
#комментарий "Update CHANGELOG.md"
#Результат получил командой "git show aefea"

#2. тег "v0.12.23"
#Результат получил командой "git log 85024d3"

#3. у коммита b8d720 2 родителя 56cd7859e05c36c06b56d013b55a252d0bb7e158 и 
#9ea88f22fc6269854151c571162c5bcf958bee2b
#Результат получил командой "git show -s --pretty=%P b8d720"

#4. Всего 8 коммитов между тегами 0.12.23 и 0.12.24
#	b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
#	3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
#	6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
#	5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
#	06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
#	d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
#	4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
#	dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
#Результат получил командой "git log --pretty=oneline v0.12.23..v0.12.24"

#5. Используя команду  "git log -S'func providerSource' --oneline"
# я получил хеш двух коммитов в которых есть данная строка, а именно 8c928e83589d90a031f811fae52a81be7153e82f
# и 5af1e6234ab6da412fb8637393c5a17a1b293663, но коммит 8c928e83589d90a031f811fae52a81be7153e82f
# создан раньше, значит в нем создана функция. 

#6. Сперва использую команду "git grep -p globalPluginDirs" 
# делее команду git log -L :globalPluginDirs:plugins.go
# и получаю коммит 78b12205587fe839f10d946ea3fdc06719decb05

#7. Командой git log -SsynchronizedWriters --oneline нашел где встречается функция и 
# через git show уведл имя автора Martin Atkins
