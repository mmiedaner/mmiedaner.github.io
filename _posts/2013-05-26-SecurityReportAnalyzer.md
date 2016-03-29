---
layout: post
title: Security Report Analyzer
category: blog
---
Many projects suffer from the lack of tooling to 
keep track of findings from penetration tests. 
Also pentesters do like to deliver the reports in 
an incompatible fashion with respect to tracking 
tools. Where do we end up with this? Yeah, you 
knew it. EXCEL !! What a marvelous tool to loose 
track of all that's important.


However, let's skip ranting and try to find a 
solution. In various projects I discovered the 
following procedure:


A penetration test is conducted and the report 
is delivered as PDF. Now the project manager / 
product owner translates the results from PDF 
to EXCEL manually and finally deposits an 
EXCEL-Sheet on a file share accessible to the 
development team. This is not only tedious but 
also highly error prawn.


How can we improve this? First let's ask the 
developers - what's their opinion? These guys 
often complain about having to deal with too 
many different ticket- and documentation systems. 
This situation does not really differ for 
the management layer. However, they are heavily 
disturbed by the lack of transparency of 
their projects.


So, let's combine these arguments to a single 
simple solution - the Security Report Analyzer. 
This simple plugin for Jira [(Atlassian)](https://www.atlassian.com/software/jira/overview). Jira is a well known issue 
tracking systems designed not only for developers. 
Given it's rich environment of plugins it is 
more than well suited to do the job. Still, 
importing data into Jira can be pain or 
an "Administrators Only" job. Both is not 
ideal for agile or small development teams. 
That made me write an additional plugin.


But first, let us go back to the initial scenario. 
You are a manager of a development team and 
have the report of a penetration test in your 
hands. On the one hand you would like to keep 
track of the findings and when they are fixed. 
On the other hand your developers roll their 
eyes when they see you presenting an 
EXCEL-Sheet. Why not asking the penetration 
tester for an XML-Export from his (her) tools 
and import that into JIRA? That is exactly 
what the Security Report Analyzer does. However, 
this plugin is a gadget that you merely place 
into your favorite dashboard. Thereby you do 
not need to be a jira-administrator nor do 
you need to move around within Jira a lot to 
find the plugin. And finally you see all the 
statistics you need right beside it: 
One place to look, one place to work.


You may wonder what about the so called 
false-positives? Yep, that is a problem. 
Within this first attempt I'll expect the 
administrator to create a certain "resolution" 
for Jira issues which will be assigned as soon 
as an issues was discovered to be a false-positive. 
The Security Report Analyzer checks if an 
issue with an identical summary and this 
special resolution exists. If this is the 
case no additional issue will be created.


The second assumption I made designing this tool, 
was that you perform a penetration test before 
you start a new release and import all findings 
in the new release. Thereby all old findings 
should be closed.


Finally this plugin is designed for JIRA 4.4.x - 
don't mess with that. Further versions will be 
compatible with higher Jira versions.


Now it's time for you to see for your self, 
if the plugin satisfies your needs. Go grab it from
[here](https://github.com/mmiedaner/security/tree/master/security-report-analyzer).

Cheers!
