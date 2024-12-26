---
LHOST: 192.168.1.50
LPORT: "4444"
RHOST: 192.168.1.100
RPORT: "1234"
PYTHONPORT: "80"
RHOSTURL: http://test
---
<%tp.frontmatter.RHOST %>
<%tp.frontmatter.LPORT %>
TEST 192.168.1.50
# <%tp.frontmatter.LHOST %>
# <%tp.frontmatter.RHOST %>
====================================Shell
sudo rlwrap nc -lnvp <%tp.frontmatter.LPORT %>

=====================================Scan
rustscan -a <%tp.frontmatter.RHOST %> -- -sCV

sudo nmap <%tp.frontmatter.RHOST %> -vvv -Pn -sCV -p- --reason -oN box.nmap

sudo nmap -Pn -n <%tp.frontmatter.RHOST %> -sU --top-ports=100

=====================================Dirb busting
dirb <%tp.frontmatter.RHOSTURL %>

sudo gobuster dir --url <%tp.frontmatter.RHOSTURL %> --wordlist /usr/share/seclists/SecLists-master/Discovery/Web-Content/common.txt

ffuf -w /usr/share/seclists/SecLists-master/Discovery/Web-Content/directory-list-lowercase-2.3-big.txt -u <%tp.frontmatter.RHOSTURL %>

feroxbuster -u <%tp.frontmatter.RHOSTURL %>

====================================Add to host file

sudo sh -c "<%tp.frontmatter.RHOST %> <%tp.frontmatter.RHOSTURL %>' >> /etc/hosts"
