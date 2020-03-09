# vsc_settings
snipets for vsc

"select from 1 p-table": {
        "prefix": "sp1",
        "body": [
            "  select @@SPID",
            "        ,t.",
            "    from M_DBO_SCHEME.[$1] f M_NOLOCK_INDEX(XPK${1})",
            "   where f.SPID = @@SPID",
            "  M_KEEPPLAN",
            "  M_ISOLAT",
        ],
        "description": "select from 1 p-table"
    },
    "select from 2 p-table": {
        "prefix": "sp2",
        "body": [
            "  select @@SPID",
            "        ,",
            "    from M_DBO_SCHEME.[$1] f M_NOLOCK_INDEX(XPK${1})",
            "   inner join M_DBO_SCHEME.[$2] s M_NOLOCK_INDEX(XPK${2})",
            "           on s.SPID = @@SPID",
            "          and s.$3",
            "   where f.SPID = @@SPID",
            "  M_FORCEORDER",
            "  M_ISOLAT",
        ],
        "description": "select from 2 p-table"
    },
    "wipe p-table": {
        "prefix": "delp",
        "body": [
            "  M_DELETE_PTABLE_INDEX(M_DBO_SCHEME.[$1], XPK${1})",
        ],
        "description": "delete from p-table by spid and index"
    }
 
 task for vsc
 
 {
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "serv FACHILD",
            "type": "shell",
            "command": "cd ${fileDirname}; ../serv ${fileBasenameNoExtension} FACHILD fatest6 dca pswd",
            "problemMatcher": [],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
